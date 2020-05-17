
# Asynchronious Programming

??HORIZONTAL

## Blocking UI

``` javascript
    var foo = $.getSync('//foo.com')
    var bar = $.getSync('//bar.com')
    var qux = $.getSync('//qux.com')

    console.log(foo)
    console.log(bar)
    console.log(qux)
```

??NOTE

* Let's assume, that we have a function that takes quite long time to finish
* and we call this function on a click event
* Tell me, what will happen?
* Will the user see any changes in the GUI?
* Will the app react to any further clicks or key strokes?
* NO - not until longRunningFunction has finished


??HORIZONTAL

<img src="asynchronious_programming/images/blockedUI.png" width="200%">



??HORIZONTAL

## Race Conditions

```Java
if (x == 5) // The "Check"
{
   y = x * 2; // The "Act"

   // If another thread changed x in between "if (x == 5)"
   // and "y = x * 2" above,
   // y will not be equal to 10.
}

```

??NOTE

* Many other programming languages have support of threading
* This means, you can run parts of that programm in parallel
* The Problem with this approach is, that when different parts of your programm
  access the same variable, very strange things can happen
* It is safe if multiple threads are trying to read a shared resource as long as they are not trying to change it.
* Multiple threads executing inside a method is not a problem in itself, problem arises when these threads try to access the same resource. Examples of shared resources are class variables, DB record in a table, writing in a file.

??HORIZONTAL

## Locking

```Java
// Obtain lock for x
if (x == 5)
{
   y = x * 2; // Now, nothing can change x until the lock is released.
              // Therefore y = 10
}
// release lock for x
```

??NOTE

* To make sure, that shared resources do not get accessed uncontrolled, you have to lock the access
* The Problem is, that it is quite likely to forget to lock or unlock a resource.

??HORIZONTAL

## JavaScript is single Threaded


??HORIZONTAL

<img src="asynchronious_programming/images/callstack.png" width="200%">


??HORIZONTAL

<img src="asynchronious_programming/images/error-in-callstack.png" width="200%">


??HORIZONTAL

<img src="asynchronious_programming/images/recursive-function-callstack.png" width="200%">


??HORIZONTAL

<img src="asynchronious_programming/images/callstack-overflow.png" width="200%">




??HORIZONTAL

<img src="asynchronious_programming/images/setTimeout.png" width="200%">

??HORIZONTAL

## Eventloop

<a href="https://www.youtube.com/watch?v=8aGhZQkoFbQ">Philip Roberts: What the heck is the event loop anyway?</a>
<hr>
<a href="http://latentflip.com/loupe/?code=JC5vbignYnV0dG9uJywgJ2NsaWNrJywgZnVuY3Rpb24gb25DbGljaygpIHsKICAgIHNldFRpbWVvdXQoZnVuY3Rpb24gdGltZXIoKSB7CiAgICAgICAgY29uc29sZS5sb2coJ1lvdSBjbGlja2VkIHRoZSBidXR0b24hJyk7ICAgIAogICAgfSwgMjAwMCk7Cn0pOwoKY29uc29sZS5sb2coIkhpISIpOwoKc2V0VGltZW91dChmdW5jdGlvbiB0aW1lb3V0KCkgewogICAgY29uc29sZS5sb2coIkNsaWNrIHRoZSBidXR0b24hIik7Cn0sIDUwMDApOwoKY29uc29sZS5sb2coIldlbGNvbWUgdG8gbG91cGUuIik7!!!">Loupe-Tool</a>

??NOTE
JavaScript solves this problem, that it runs several Threads from the beginning, but you as programmer
never get in touch with them. Instead you just write code that gets evaluated immediately or you write
code that will be evaluated on a specific event.
We already practices that, when we applied click handlers for example.

??HORIZONTAL

## Callback Hell

```JavaScript
const fs = require('fs');

fs.readFile('DATA', 'utf8', function(err, contents) {
    if (err) {
        // do something about the error
    } else {
        const settings = parse(content)
        settings.forEach(function (url) {
            request(url, function (err, contents) {
                if (err) {
                    // do something about the error
                } else {
                    const data = parse(contents)
                    fs.writeFile(data, 'utf8', function (err, contents) {
                        // ...
                    })
                }
            })
        })
    }
});

```

??NOTES

Now if you need to do things that depend on each other, and each has to be
done asynchroniously, how would you do that then?

Let's have a look at an example of nodejs, but it could be the same for any set of asynchronous tasks that depend on each other. In this example, we read a file asynchronosly. In the Callback we parse the content of that file, just read another file from that. For example if you have a config file for your server which specifies which URLs have to be loaded.
And loading these URL will result in storing their contents in new files.

Then you have a callback calling a callback and so on and so forth.

??HORIZONTAL

## Work with Promises

``` JavaScript
const fs = require('fs');

fs.readFilePromise('DATA', 'utf8')
    .then((content) => {
        const settings = parse(content)
        return Promise.all(settings.map(requestPromise))
    })
    .then((listOfContents) => {
        const promisedFileState = listOfCntents
            .map(parse)
            .map(fs.writeFile)
        return Promise.all(promisedFileState)
    })
    .then((listOfState) => {
        // ...
    })
    .catch((err) => {
        // do something about the error
    })
});

```

??NOTES

So you see, that this is quite an uncomfortable way of coding. There must be a better way to create more complex asynchronious calls, so that you do not loose mind over it.
The key idea is the so called promise. It is what it says a promise that something will happen in the future. Let us assume, that there is a version of each longterm operation we called in the example above that returns us a promise, a kind of voucher if you will. And we can attach a note to the voucher or even better a magic spell, a course to it, that will fullfill in the future. Just like "Sleeping Beautiy" that fell a sleep on her 15th Birthday, just as the which has coursed to her.

We only have to catch the error one time. We can seperate the future curses from each other and put them into functions of their own and maybe reuse them...

??HORIZONTAL

## Promisify a function

``` JavaScript
const myTimeoutPromise = (timeToWait) => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            try {
                return resolve(timeToWait);
            } catch (err) {
                return reject();
            }
        }, timeToWait)
    })
}

myTimeoutPromise(5000)
    .then((time) => {
        // do something after <time> seconds
    })
    .catch(() => {
        // handle error
    })
```

??NOTE
Since the Promise-API is so helpful, it is a blessing that we can turn anything into a promise if we want to.
To do so, you have to call the longterm function inside of a Promise. Promise awaits function, that gets two functions as input. The first one is called resolve, it is what gets called in the .then-block. And a reject function that should be called if an error happens. This will evaluate the .catch-block().


??HORIZONTAL

## Combine Promises

``` JavaScript
var promise = Promise.all([
    myTimeoutPromise(2000),
    myTimeoutPromise(5000),
    myTimeoutPromise(1000)
])

promise.then((data) => {
    console.log('How long have I been waiting?')
    console.log('What does data contain?')  
})
```

??NOTE
If you have several more or less independent promises but you need their results all at the same time, how could you do that? For this we have the static method Promise.all(). It Takes an array of promises, and awaits them. When the last of the promises resolves, it will resolve as one and will provide an array of all promise results.

??HORIZONTAL

# And even simpler

``` JavaScript 

async function deferredLog (timeToWait, text) {
    await myTimeoutPromise(timeToWait)
    console.log(text)
}


```

??NOTES
But even Promises can be complex, because everything has to happend in a .then()-block.
You can simplify the usage of Promises a lot by async/await. 

So if you have a function, that will handle a promise, you should mark it with the keyword.

And to access the data from a promise you should use await. And by that, your method looks almost like being programmed single threaded completely.



??HORIZONTAL

## To be continued


??HORIZONTAL

## Fetch

``` JavaScript
const url = '...'
fetch('url')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch((err) => console.log("ERROR: ", err))
```

??NOTE
One usecase from where you probably will meet promises is loading data from the net.
It dosen't matter if you call some real dynamic data from any kind of API

??HORIZONTAL

## Fetch Mock

??NOTE

example testing it

??HORIZONTAL

## CRUD & Rest

* GET
* POST
* PUT
* DELETE