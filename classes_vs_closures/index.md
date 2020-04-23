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
## Summery on Classes

* Classes associate Data with Functionality
* Classes are a way to organize your code
* Classes represesent state

If you want to use Classes, you should read [Design Patterns from Gamma at al.](https://www.amazon.de/Design-Patterns-Object-Oriented-Addison-Wesley-Professional-ebook/dp/B000SEIBB8/ref=sr_1_1?__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&dchild=1&keywords=design+patterns&qid=1587445230&sr=8-1)

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
function createFn() {

}
```

??NOTES
* pure functions
* higher order functions
* currying
* functional composition // far beter as
* when to use classes in JavaScript, when to use closures
    -- When framework x is forcing you to use classes
    -- When you need to instanciate a lot from it like 1000 dots a coordinate system
    -- Otherwise use closures :D
