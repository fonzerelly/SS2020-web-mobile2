# Asynchronious Programming

??HORIZONTAL

``` javascript
    const longRunningFunction = () => {
        // some very complex logic
        ...
    }

    document.getElementsById('myButton')
        .addEventListener('click', longRunningFunction)
```

??NOTE

* Let's assume, that we have a function that takes quite long time to finish
* and we call this function on a click event
* Tell me, what will happen?
* Will the user see any changes in the GUI?
* Will the app react to any further clicks or key strokes?
* NO - not until longRunningFunction has finished

??HORIZONTAL

## JavaScript is single Threaded

??NOTE

* Many other programming languages have support of threading
* This means, you can run parts of that programm in parallel
* The Problem with this approach is, that when different parts of your programm
  access the same variable, very strange things can happen

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

??HORIOZONTAL

## Eventloop

??NOTE
JavaScript solves this problem, that it runs several Threads from the beginning, but you as programmer
never get in touch with them. Instead you just write code that gets evaluated immediately or you write
code that will be evaluated on a specific event.
We already practices that, when we applied click handlers for example.

??HORIOZONTAL

## Callback Hell

```JavaScript
const fs = require('fs');

fs.readFile('DATA', 'utf8', function(err, contents) {
    if (err) {
        // do something about the error
    } else {
        console.log(contents);
    }
});

console.log('after calling readFile');
```

??HORIZONTAL

## Promises 

??NOTE
With setTimeout

??HORIOZONTAL

## Promisify a callback

??HORIZONTAL

## Work with Promises

??NOTE
Example with .then and reject

??HORIZONTAL
## Combine Promises

??NOTE
Promise.all()

??HORIZONTAL
## Fetch

??NOTE
Example about how to use Fetch

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