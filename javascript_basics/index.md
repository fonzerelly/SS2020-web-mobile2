# JavaScript Basics

??NOTE
* As we already mentioned there was a lot of movement in this upcoming internet technology. The browser wars were raging, because http was the first internet technology, that had the potential to be used by the normal user. Netscape has always been the underdog, but it had been working on the internet technology area long before Microsoft realized, how important the internet would be. It took Microsoft about a year to implement Internet Explorer, while Netscape released every three months a new but maybe incomplete Product. So they were more or less the first company to work in an agile way. But when Microsoft came up with IE, Netscape had to bring a really novelty to the browser to keep also their partnership with sun microsystem, who wanted  to position Java as the Internettechnology. 
This ment for Brandon Eich, an experienced Software Developer of Netscape that he would had to implement a programming language for the web in ONE Sprint. A Programming language, that had not the need to be compiled but could be interpreted, so that you can directly see the effect of your code onto the HTML that evan should be easy to learn. 
The outcome was a programming language, that was not only a toy language although it was as easy to learn.  It was also a language with highly advanced concepts, that are not too obvious.  And the only thing that it shared with Java was some Syntaxdetails, like the curly braces, as they have been used in Java and C/C++. In fact Eich had Schema in mind when he wrote JavaScript, a highly functional language. And we will see later, that this is characteristic of JavaScript as well. 

## Why JS is different
Today we can more or less say, that JavaScript succeeded. JavaScript fulfiled the Promise, that Java once gave: To run merely everywhere. 
* It runs on every desktop since it every desktop has a browser.
* It runs on many servers, since NodeJS was available
* Its default Data-Format JSON is so deployable, that the new nosql based Database Systems mongodb, couchdb, ...
* There are even microcontrollers that run javacript 
And it is so easy to lern, that even without much programming experience you can achieve very fast  good results.


??HORIZONTAL
## Variables
``` javascript
    a = 1 // EVIL!!!
```

??HORIZONTAL
## Variables
``` javascript
    var a = 1 // Deprecated 
```

??HORIZONTAL
## Variables
``` javascript
    let a = 1
```

??HORIZONTAL
## Variables
``` javascript
    const a = 1;
    a = 2 // TypeError: Assignment to constant variable.
```

??HORIZONTAL
## For what do I need variable?
I want to memoize some data

??HORIZONTAL
## Numbers
``` javascript
    const a = 1;
    const b = 3.14;
    const c = Infinity;
    const d = -Infinity;
```

??HORIZONTAL
## For what do I need Infinity?

When I generically have to find the minimum in a list:

``` javascript
    var myList = [1]
    // instead of cumbersomly check for the length
    if (myList.length == 1) {
        return myList[0]
    } else {
        return min(myList[0], myList[1])
    }
    // I can simply
    myList.concat([Infinity])
    return min(myList[0], myList[1])
```


??HORIZONTAL
## Falsy values
``` javascript
    const a;        // undefined (accidentally)
    const b = null; // intended
    const c = 0;    // casted to false
    const d = '';   // casted to false
    const e = NaN;  // 'Not a Number' happens e.g. here
                    // 5 - 'any string'
```

??HORIZONTAL
## For what do I need null?
To clearify that you really did not want to store some data here.

??HORIZONTAL
## Strings
``` javascript
    const double_quoted = "Here I can use ' to mark strings"
    const single_quoted = 'Here instead " is valid as well'
    const escaped = 'Although I can \'Escape\' as well'
    const also_escaped = "Same is \"true\" for doublequoted"
```
??HORIZONTAL
## For what do I need two types of quotes?
To use single quotes inside of HTML attributes which are already surrounded by double quotes.

??HORIZONTAL
## Template Strings
``` javascript
    const name = 'Ansbach'
    const greeting = `Hello ${name},
        today we learn JavaScript.`
```

??HORIZONTAL
## For what do I need Template strings
To not have to cumbersomly concatenate lots of strings...

??HORIZONTAL
## Arrays
``` javascript
    const myList = [1,2]
    const newLength  = myList.push(42)  // myList == [1,2,42]
    const one        = myList.shift()   // myList == [2,42]
    const fourtyTwo  = myList.pop()     // myList == [2]
    const two        = myList[0]
```

??HORIZONTAL
## For what do I need push and pop?
To easily implement a stack.

??HORIZONTAL
## Arrays
``` javascript
    const myList = [1,2,3,4,5,6,7,8,9]
    const extract = mylist.slice(2,4)   // [3,4]
    const concatenated = mylist  
        .concat(extract)                // [1,2,3,4,5,6,7,8,9,3,4]           
    const aString = mylist.join(' ')    // "1 2 3 4 5 6 7 8 9"

```

??HORIZONTAL
## For what do I need slice or concat?
To not have to call push and pop infinit times

??HORIZONTAL
## Functions
``` javascript
    function name () {
        return 'Max Mustermann'
    }
    const anonymous = function () {}
    const inc = (x) => x + 1            // simple Arrow Function 
                                        // implicitly returns last 
                                        // statement

    const safeHead = (list) => {        // when creating complex 
        if (list.length === 0) {        // anonymous functions
            return null                 // in curly braces,
        }                               // you have to use
        return list[0]                  // return
    }
```

??HORIZONTAL
## For what do I need functions?
To abstract parts of your algorithm away so that you do not have to think about them anymore!

??HORIZONTAL
## Function Parameters
``` javascript
    const add = (a, b) => a + b
    const toArray = (...args) => args   //spread
    
    add(1)              // NaN because b was undefined
    add(1,2,3,4,5,6,7)  // 3 because the other parameters 
                        // are just ignored
```
## For what do I need that ...args thing
To access an infinit number of parameter without converting them from arguments to an array.

??HORIZONTAL
## Objects
``` javascript
    const literal = {
        property: 42,
        method: function () {},
    }
    const fortyTwo = literal.property // by point operator
    const accessString = 'property'
    const fortyTwo2 = literal[accessString] // by accessString 

    const result = literal.method()
```
??HORIZONTAL
## For what do I need Objects
To store data together that belong together in a named way.
To prvent switch - case - statements

??HORIZONTAL
## JSON
``` JSON
{
    "name": "Max Mustermann",           // Note, that the keys have
    "address": {                        // to be in doublequotes
        "city": "00001 Exempelstadt",   // values may be plain 
        "street": "Beispielstrasse",    // for numbers and booleans 
        "nr": 19                        // Methods are NOT allowed
    },                                  // in JSON-Format
    "platin-user": true                 
}
```

??HORIZONTAL
## JSON
``` javascript
    const user = JSON.parse(data)
    const name = user.name
    const addressString = JSON.stringify(user.address)
```

??HORIZONTAL
## For what do I need JSON?
To retreive data from the server in a way that JavaScript can handle by default (same as objects)


??HORIZONTAL
## Classes
``` javascript
class MyClass {
    constructor(a) {
        this._a = a
    }
    set a (v) {
        this._a = v
    }
    get a () {
        return this._a
    }

    // This method is only available on instances
    method () {} 
}

// This method is always available
MyClass.prototype.staticMethod = () => {}
```

??HORIZONTAL
## Instance
``` javascript
const myInstance = new MyClass(42)
myInstance.a        // accesses _a via the getter
myInstance.a = 21   // modifies a via the getter

myInstance._a       // But accessing _a directly is also possible!
```

??HORIZONTAL
## For what do I need classes?
For team mates that only know OOP and don't know better... :D

??HORIZONTAL
## if-else
``` javascript
    const k = 3
    let result
    if (k % 3 === 0) {
        result = 'valid'
    } else {
        result = 'invalid'
    }
    
    // DO NOT CASCATE THIS
    const result2 = (k % 3 === 0) ? 'valid' : 'invalid'
```

??HORIZONTAL
## For what do I need if-else?
When you so no otherway to separate usecases

??HORIZONTAL
## switch-case
``` javascript
    const fruit = 'banana'
    let price
    switch (fruit) {               // can you see the problem here?
        case 'orange':
``` javascript
const a = 1
if (a == '1') {
    // you would not expect that this evaluates here
    // but due to type type casting it will
}

if (a === '1') {
    // tripple equal
            price = 0.59
            break;
        case 'banana':
            price = 0.48

        case 'apple':
            price = 0.32
            break;
        default:
            throw new Error('unknown fruit type')
    }
```

??HORIONTAL
## For what do I need switch-case?
You don't...

??HORIZONTAL
## preferred switch-case
``` javascript
    const fruit = 'banana'
    const pricePerFruit = {
        orange: 0.59,
        banana: 0.48,
        apple: 0.32
    }
    const price = pricePerFruit[fruit]
    if (!price) {
        throw new Error ('unknown fruit type')
    }
```

??HORIZONTAL
## for-loop
``` javascript
const myList = [1, 2, 3, 4, 5]

for (let i=0; i<myList.length; i++) {
    const entry =  myList[i]
    // do something with entry
}
```

??HORIZONTAL
## For what do I need for-loops?
For usecases, where the acces to a list
needs to be calculated somehow (rarly...)

??HORIZONTAL
## while-loop
``` javascript
var game_running = true
function stopGame () {
    game_running = false
}
while (game_running) {
    // loop until user event
}
```
??HORIZONTAL
## For what do I need while-loops?
For use-Cases where I don't have numerical end conditions

??HORIZONTAL
## do-while-loop
``` javascript
const myList = [1, 2, 3, 4, 5]
let i = myList.length
do {
    const entry = myList[--i]
    // do sometihng with entry
} while (i > 0)
```

??HORIZONTAL
## For what do I need a do-while-loop
When I want to be sure, that the loopcontent gets executed at least one time

??HORIZONTAL
## for-in-loop
``` javascript
const myObj = {a: 1, b: 2, c:3}
for (var key in myObj) {
    const value = myObj[key]
    // do something with value
}

```

??HORIZONTAL
## For what do I need a for-in-loop
When I want to iterate over Object attributes

??HORIZONTAL
## forEach
``` javascript
const myList = [1, 2, 3, 4, 5]

// if you just need to do something
// with each entry in a list

myList.forEach((entry, index, array) => {
    // do something                         
})
```

??HORIOZNTAL
## For what do I need a forEach loop?
* When you want to prevent classic for-loops
* When you want to use a function already in use where else to handle on 
??HORIZONTAL
## map
``` javascript
const myList = [1, 2, 3, 4, 5]

// if you want to create a modified copy
// of you list
// here it results in [2, 3, 4, 5, 6]

myList.map((entry, index, array) => {   
    // create modified version of entry 
    return entry + 1                    
})
```

??HORIZONTAL
## For what do I need .map?
To create a new modified version of an array

??HORIZONTAL
## filter
``` javascript
const myList = [1, 2, 3, 4, 5]

// if you want to create a copy of your 
// list, where all entries are removed that
// do not fullfill a characteristic [2, 4]

myList.filter((entry, index, array) => {   
    // check a characteristic of the entry 
    return entry % 2 === 0 // boolean
})
```

??HORIZONTAL
## For what do I need .filter?
If I want to create a version of an array without some
unwanted entries

??HORIZONTAL
## reduce
``` javascript
const myList = [1, 2, 3, 4, 5]

// if you want to boil down an array
// to one value completely different
// from its former structure
// here we create the sum 15

const neutralValue = 0;
myList.reduce((accumulated, entry, index, array) => {
    // combine accumulated value with enty
    return accumlated + entry
}, neutralValue)
```
??HORIZONTAL
## For what do I need reduce?
With reduce you can transform a list into anything.
But don't - use forEach or map instead. reduce is too 
complicated


??HORIZONTAL
## Decomposition and the spread operator
``` javascript
const [a, b] = [1, 2, 3]            // a = 1, b = 2

const {c} = {a: 1, b: 2, c: 3}      // c = 3

const myList = [1, 2, 3]

const newList = [...myList, 4, 5]   // 1, 2, 3, 4, 5

const myObj = {a: 1, b: 2}

const newObj = {...myObj, c: 3}     // {a: 1, b: 2, c: 3}

const newObj2 = {a, b, c}           // {a: 1, b: 2, c: 3} uses the 
                                    // local variablename as key
```

??HORIZONTAL
## For what do I need the spread-operator
You can clone objects, which is very important to not scramble up state by side effects.

??HORIZONTAL
## Named Parameters by decomposition
``` javascript
const a = 1
const b = 2
const c = 3

/* you never know what a, b and c are */
const aFunction = (a, b, c) => {}

aFunction(b, c, a) // such a mistake might be hard to find

 /* here the params do not depend on the order */
const fnWithNamedParams = ({a, b, c}) => {}

fnWithNamedParams({b, c, a}) // here the order does not matter, 
                             // since the values are sorted properly
                             // by decomposition to their names
```

??HORIZONTAL
## For what do I need named parameters?
Without named parameters, there is the risk that you mix
up the order of function parameters:

``` javascript
const appendSumToString(str, num1, num2) {
    return str + (num1 + num2);
}
appendSumToString("kg ", 5, 3) // kg 8
appendSumToString(5,3, " kg") // 53 kg 
```

??HORIZONTAL
## == is not the same as ===
``` javascript
const a = 1
if (a == '1') {
    // you would not expect that this evaluates here
    // but due to type type casting it will
}

if (a === '1') {
    // tripple equals do not cast the type
    // so prefere to use tripple equals
    // this would not be evaluated
}
```



??NOTE
Flaws in a Programming language are things that make the reading of a programming language unintitive.
For example from other languages like java you already know that finding the equality of two things is not that easy as it sounds. When you apply == in Java to two variables and those variables carry only basic datatypes like integers or boolean, then you can be sure, that this operation returns true if those values are equal and false if they are not.

Not so in JavaScript. Here the data gets casted to a fitting datatype. It tries to be helpful and prevent exceptions as good as possible. Unfortunately this leads to unintuitive code and to logic errors that might be hard to find.

Therefore please do not use double equals, prefere tripple equals instead.

??HORIZONTAL
## 1 + '2'
``` javascript
const a = 1 + '2'   // '12'
```
??NOTE
Similar is the problem of the undecidable + operator. + in context of number of course mean
addition. so 1 + 2 equals 3. And you can also concatenate strings by the plus operator.  
BUT would happen, when you try to add a number and string. Here the number gets casted into a string and both strings get concatenated to the string '12'. This is also an error that is hard to track down.
