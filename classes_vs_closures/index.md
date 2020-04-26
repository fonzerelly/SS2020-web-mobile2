# Classes vs Closures

??HORIZONTAL

## Why do you need to know about this?
* You need to know your tools!  <!-- .element: class="fragment" -->
* You need to know the gotchas!  <!-- .element: class="fragment" -->
* You need to know how to decide!  <!-- .element: class="fragment" -->

??NOTES

Probably once upon a time, you hang up a picture to a wall. You might have done it with a hammer and a nail. Or you choose to use a power drill, a dowel and a screw. So there are several options to solve the problem of hanging a picture to a wall. So you need to know your Tools to know about the available options.

Depending on what solution you take for the goal of hanging a picture, there are several gotchas that can happen to you. You might bend a nail by hitting it. The wohle you drill might be of the wrong size. The screw or nail in the wall might brake. You need to know the gotchas to estimate a risk for an option.

And depending on the circumstances, like the weight of the picture, the wall plaster, steel beams in the wall, you might select a different approach. For example for a small foto, you would take a nail and a hammer. Or if the image has more weight, you might turn to the more complicated aproach and use a drill, a dowel and a screw instead.  You can only decide if you know as much as possible about your tools and the circumstances of your problem.

??HORIZONTAL

## Object Orientation

??NOTES
In classic programming languages like Java or C# we find the ObjectOriented Concept. It is said, that it's main idea means to represent things of the real world in software. This is a simplification to grasp the basic idea, but it is not the real truth. The reason why we do OOP is, having better controll on software. Than controll manifests in these four principles:

??HORIZONTAL

## Abstraction

<img src="classes_vs_closures/images/Abstraction.jpg">

??NOTES
Abstraction: When somebody in my company already created something like an Account, I do not need to invent another account. I can just use that Account-Class to create my own account. So the complex nature of an account is abstracted away for me and I can take care of a newer feature, that only builds upon accounts. Please realize, that the word "abstract" in our daily usage has often another meaning. We often think that "abstract" is another adjective for "complex". But it is the other way round. The latin root ment "remove" and  in computer science this boils down to: "simplify, only work with the basic idea, not the complex details of it".

??HORIZONTAL

## Inheritance

<img src="classes_vs_closures/images/Inheritance.jpg">


??NOTES
Inheritance: Another Idea coming from ObjectOrientation is the easy reuse of code. One of the ways to do so is the so called inheritance. It means to create a parent class like "Shape" and derive from it some common attributes and methods used in all shapes. A descendant of a "Shape" could be rectangle, which only implements the specifics of a rectangle. BUT BE CAREFUL! A wrong believe in to the usage of inheritance can lead to the violation of Livskovs Substitution principle. In case of a "Shape", it would be wrong to derive a "Square" from a "Rectangle". When you set the width and height of rectangle to be equal it will not turn its type into a square and vice versa. If you then need to find all Squares in a list will be much complexer then by filtering by its type.

??HORIZONTAL

## Encapsulation

<img src="classes_vs_closures/images/Encapsulation.jpg">

??NOTES

Encapsulation: When you allow access to any variable and method, it will be hard to keep controll of the source code. For example, when you have a global variable to keep some intermediate calculation result, there is a chance that somebody will "reuse" that result, so that she/he does not have to come up with the calculation her/himself. If you then find a better way to calculate the result without an intermediate result, cou can not delete that variable because you would break that other persons code. It might force you to maintain your old code even, although you this better new way would realize a new feature.
Such a scenario must not happen. Therefore Encapsulation mean, that in OOP, you have tools in the Programming Language to prevent such a missuse of your code.

??HORIZONTAL

## Polymorphism

<img src="classes_vs_closures/images/Polymorphism.jpg">

??NOTES

Polymorphism: Some things can be seen in different ways. If a class provides serveral "is-a-"-relationships it is polymorphic. There are different ways to achieve that, depending in which programming language you work. Polymorphism in every day life can be seen for example in a coffee-machine. It needs water and a coffee pad. But depending on the coffey pad, the machine can create classic coffey, mocha, latte, cappuccino, ... So the cofee-maschine is Polymorphic and can also be a Mocha Machine, a Latte Machine, a Cappuccino Machine, ...

??HORIZONTAL

## Prototypal Inheritence

``` JavaScript
function Person(firstName, lastName) {
    // this points to;
    this._firstName = firstName;  //_... signals privacy but 
    this._lastName = lastName;    // there is no guarantee 
                                  // that somebody ignores 
                                  // that

    // with new it's like "return this;"
}

Person.prototype.alertAllData = function() {
    alert (this._firstName + ' ' + this._lastName);
}

const p = new Person ('Helmut', 'Roderus');

p.alertAllData() // "Helmut Roderus"
```

??NOTES
Classic Inheritence works in a very philosophic way. Classes are mere ideas and onle objects as their instantiations exist in the real world. The classes are also the abstract types which. Not so in JavaScript, here you don't have Types. Every Object is a copy of another.
In this example here on new a copy of Person.prototype gets created and this-variable in the Person-Constructor points to this copy. The Constructor-Function "Person" applies the parameters firstName and lastName to it and the new object, which got stored in "p".
When getFullName gets called on p, the "this"-pointer points to p and by that accesses the values "Helmut" and "Roderus" to output "Helmut Roderus".
The underscore in front of those variable names is a convention to signal that these are private and must not be accessed from outside. In Java you would write private in front of it and the compiler would not allow you access from outside of the object. In JavaScript there is nothing to prevent you from doing so.

??HORIZONTAL

## Loosing Context

``` JavaScript
setTimeout(p.alertAllData, 1000);  // this points to the global context "window"
                                   // result in "undefined undefined" after one
                                   // second
```

??NOTES
But be careful! In JavaScript you can pass Methods as parameters. If you do so, the "this"-keyword looses its context. So in this example, the this-keyword looses the context of p and uses the global context instead, which in the browser is the window-object.

??HORIZONTAL

## Syntactic suger

```JavaScript
class Person {
    constructor(firstName, lastName) {
        this._firstName = firstName;
        this._lastName = lastName;
    }

    alertAllData() {
        alert(this._firstName, this._lastName)
    }
}
```

??NOTES
This prototype-thing is a little awkward to write. Since ES6 there is a nicer way to define a class. But still the same prototypal inheritance mechnanism works under the hood. So you better need to understand prototypal inheritance when you want to apply to OOP.

??HORIZONTAL

## Derivation

``` JavaScript
class Employee extends Person {
    constructor (firstName, secondName, salary) {
        super(firstName, secondName);
        this._salary = salary;
    }

    alertAllData() {
        super.alertAllData();
        alert(this._salary);
    }
}
```

??NOTES
If you want to build upon an existing class and extend its functionality, you will do so with the keyword "extends". By that your class contains the same attributes and methods as the parental class. And it defines additional methods with it.
You can call the parents constructor by the super-keyword and pass the relevant parameters to it. Same goes if you want to overwrite parents methods and need to run their code first.


??HORIZONTAL

## Delegation over Inheritance


``` JavaScript 
class CompanyCar {
    ...
    getOdometerCount() { ... }
    enterLogbookEntry(journeyReason, kilometersTraveled) {
        this.logbook.store(Date.now(), journeyReason, kilometersTraveled);
    }
}

class Employee extends Person {
    constructor(firstName, secondName, salary, companyCar) {
        ...
        this.companyCar = companyCar;
    }

    registerJourney (journeyReason, kilometersTraveled) {
        this.companyCar.enterLogbookEntry(journeyReasen, kilometersTraveled)
    }

}
```


??NOTES

As already mentioned, it can be become a big problem, if you only try to share code by derivation. In fact I see it now as an anti pattern, that only in a few cases make sense. Most of the time I prefer delegation, which means: Most of the time you are better of by putting functionality into another class and using it from there.
Here for example, we created a new class CompanyCar, that might be connected to a database for example that not only stores the logbook data of a CompanyCar, but also the OdometerCount. Based on that the company can differentiate between how much the car was used in personal use.

To decide between inharitance and delegation, you should think about the problem you are about to model. Does the new functionality you want to build really fit to the nature of the class you want to add it? For example, we could have implemented the enterLogbookEntry-Method also on the Employee-class. But is this feature really something that belongs to the typical aspects of an employee? For example, the employee is usually not directly connected to the database-table of CompmanyCars, since not every employee has a companyCar. So that the decision for delegation here seems to be appropriate. But the judgment about this questions may be different according to the problem setup.

??HORIZONTAL
## Summery on Classes

* Classes associate Data with Functionality
* Classes are a way to organize your code
* Classes represesent state

??NOTES

In the case of the CompanyCar, I even think that the delegation to a CompanyCar might only be a stopgap solution. Probably we should have implemented a Decorator-Class that connects the Employee with the CompanyCar. And the functionality to provided to the User would have been implemented there. 
More on recipes like the Decorator, you can find in [Design Patterns from Gamma at al.](https://www.amazon.de/Design-Patterns-Object-Oriented-Addison-Wesley-Professional-ebook/dp/B000SEIBB8/ref=sr_1_1?__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&dchild=1&keywords=design+patterns&qid=1587445230&sr=8-1). If you want to do ObjectOriented Programming, you need to read this. It will give you some ideas about how to handle specific problems and even  more important, it gives you a vocabulary to discuss with other Software-Engineers about aspecific solution.

??HORIZONTAL

## The DRY-Principle

??NOTES

So why is the discussion about deligation or inheritance so important? Well some algorithms can be very complex. And the efford to reinvent that algorithm again, to use it somewhere else seem to be quite easy by just copying it. BUT this is a very bad solution, especially when you copy the same code more than two times. What will happen, if you find an error in that complex algorithm? You would have to repair the same bug at all places, where you copied it and it is very likly that you forget once occurance of that code. In addition, somebody else might have changed one occurance of that algorythm but not the others to achieve something slightly different. But the Bug you need to fix occurs in that modified version of the algorithm as well, and it might be impossible to find that occurance as well.
To prevent this, ensure that you follow the DRY-Principle: "Don't repeat yourself". Although it might seem to be easier to copy and paste the code, there are better ways like deligation or derivation. But soon we will see even better ways to reuse code. But as a rule of thump: If you find you need the same code more than two times, then you should spend the efford to move that code to a new class or method.

??HORIZONTAL

## Lifetime of function variables

``` JavaScript
                                            // greeting not existent
    function greet (name) {                 // |
        const greeting = "Hello";           // greeting carries "Hello"
        return greeting + " " + name;       // |
    }                                       // greeting not existent

    const userGreet = greet("Helmut");
```

??NOTES
Usually, greeting when you defnine Variables in Functions these Variables exist only inside the function. Like in this example: We define a function, but the variable inside is not yet instantiated. But when we invoke greet, the code of greet gets evaluated and in the first line of it, the Variable "greeting" gets declarated and set to "Hello". As long we are inside of the function, the memory for Hello is allcoated. But as soon as we leave the function with return,
greeting gets deleted from memory again.

??HORIZONTAL

## Closure

```JavaScript
const createPerson = (firstName, lastName) => {  // firstName and lastName exist
    return {                                     // |
        alertAllData: () => {                    // |
            alert(firstName + " " + lastName);   // |
        }                                        // |
    }                                            // |
}                                                // | ...

const p = createPerson("Helmut", "Roderus")      // firstName set to "Helmut
                                                 // secondName set to "Roderus"
                                                 // |
p.alertAllData()                                 // Alerts "Helmut Roderus"
```

??NOTES
But this does not necessary need to be in JavaScript. When you return an Object from a function, that's methods refer to the variables that are known inside of the functions scope, those variables will not be deleted and kept inside a so called closure. By that you can create objects with REAL private data, that can not be accessed from outside. This kind of programming is not OOP it is called "Functional Programming".

??HORIZONTAL
## Functional Programmming

* is possible when functions are first-class-citizens  <!-- .element: class="fragment" -->
* tries to prevent state as far as possible to prevent so calles side-effects  <!-- .element: class="fragment" -->
* does not need design patterns. Most of what design patterns give you for classes is a peace of cake with Functional Programming

??HORIZONTAL
## Pure Functions


``` JavaScript
// pure function
function add (a, b) {
    return a + b;
}

add(1,2) // 3

add(3,4) // 7

// impure function
Math.random() // 0.14567
Math.random() // 0.9756

//random depends on state, like dates
```

??HORIZONTAL

## Higher Order Functions


``` JavaScript
function process(fn, p1, p2) {
    return fn(p1, p2)
}

function add (a, b) {
    return a + b;
}

const result = process(add, 2, 3)          // 5
```

??NOTES
Higher Order Functions are Functions that can take functions as input parameters
and or return functions as result parameters.

In this example we use the HigherOrder Function process(), which takes a function and two parameters. It returns the result of the two parameters applied to the passed in Function. In this example we pass the function add and
the parmeters 2 and 3. Of course this results in 5.

Maybe HigherOrder Functions already reminded you of Polymorphism, since process could do different things depending on what you pass in, just like the already mentioned CoffeMachine.

??HORIZONTAL
## Currying I

``` JavaScript
function simplifiedCurring (fn) {
    return function (a) {
        return function (b) {
            return fn(a, b)
        }
    }
}

function add (a, b) {
    return a + b
}

const curriedAdd = simplifiedCurring(add)

curriedAdd(1)(2)                            // 3
curriedAdd(1, 2)                            // Function expecting another parameter

const increment = curriedAdd(1)

increment(4)                                // 5
```

??NOTES
Now when you push that idea a little further, you might come up with what we call currying. The Basic idea is this: What if you could store some parameters of a function with it, so that some parameters stay open and others don't?

In this example we have a function simplifiedCurring, that takes a function and
returns a function. But even weirder the returned function does the same, just as its output. So when you call simplifiedCurring with add, you will get a function that only takes one argument. This leads to this weird seeming syntax
with braces after braces. But in fact what happens is, that we create a new function here that stored the value 1 for a of the add function. And b is still not defined. So by calling the result of that function with a value, we specify be.

Now what is add with a fixed parameter of a to 1? It is an increment function.
Every value you pass it in, it increments by one and returns that value.

??HORIZONTAL

## Curring II

``` JavaScript
const R = require('ramda')

function add (a, b) {
    return a + b
}

const curriedAdd = R.curry(add)
curriedAdd(1)(2)    // 3
curriedAdd(1, 2)    // 3

cosnt increment = curriedAdd(1)
```

??NOTES
Now instead of using simplifiedCurry you can use a curry-function from a library like Ramda or lodash. Instead of our simplifiedCurry-Function that only could handle two parameters, the more advanced version from a librlary can handle an unlimited amout of parameters.
By that, you can make from every what so ever complex function simplified versions specific to one use case.
Can you already see how we could easily reuse or simplify function by curring alone?

??HORIZONTAL

## Functional composition

``` JavaScript
const add = R.curry((a, b) => a + b)
const isEvan = (x) => x % 2 === 0
const isOdd = R.not(isEvan)

function isNextOddClassic (num) {
    const nextValue = add(1, num)
    return isOdd(nextValue)
}

const isNextOdd = R.pipe(add(1), isOdd)

isNexOdd(4)                          // true
isSumOdd(5)                          // false
```

??NOTES

Functional Composition now brings all together and gives you a far more advanced way to reuse code. You can pass a compose-function several functions and it will it call each by the result of the other.

Let's have a look at a simple example: We want to write a function that can tell us if the next number of a value is odd nor not. So we base our work on an add-function and an isOdd-Function, that by the help of the helper R.not was gained from isEvan.

The classic way to solve it, would be writing a new function isNextOddClassic and inside of it
calling isOdd() with the result of add stored in nextValue. Things like that you see often in OOP-styled languages, where you create a class, store it in a temporary variable and pass that variable to another class, which will be used by another class. In Functional Programming, when you use composition, the handlich of such a thing is far easier to implement and read:

You call R.pipe with the functions you want to be evaluated by it from left to right. Please note, that add is curried and by that, add(1) will return a function taking only one parameter to be incremented by 1.


??HORIZONTAL

## Closures over Classes in JavaScript

* When a framework (like Angular) forces you to use classes  <!-- .element: class="fragment" -->
* When you need to instantiate a lot of instances of it. (like 1000 dots in a coordinate system)  <!-- .element: class="fragment" -->
* Wheny your team knows only OOP (which is unfortunately the most common reason) <!-- .element: class="fragment" -->

??NOTES

So from my point of view Closures are superior to Classes in most cases. There are a few usecases where you should prefer classes.
For example when you use a framework that forces you to use classes. Angular is for example extremly connected to classes, since they use Annotations and use Types for Dependency Injection.
Or when you need to instantiate a lot of instances from it. For example when you need to model lots dots in a coordinate system. As it turns out closures are slightly slower than classes, but only has an effect on a big number of instances.
And the most important reason why you have to use Classes (which is unfortunately the most common usecase) when you team only knows OOP.
