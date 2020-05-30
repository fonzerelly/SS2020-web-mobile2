
# Frameworks - an overview

??HORIZONTAL

## Why you should use a framework

* Abstracting the Browser away  <!-- .element: class="fragment" -->
* Simplifies 2-Way-Data-Binding  <!-- .element: class="fragment" -->
* Provides Build-Chain  <!-- .element: class="fragment" -->

??NOTES

There are several reasons why you should use a Framework:

First of all, it abstracts the Browser away. In the early days the browsers creators fought hard to give their products a unique selling point, very often for the price of incompatibility. It was quite a hassle for web developers, to ensure their web pages works for every browser.

Another thing is the so called 2-Way-Data-Binding (create example live) This can be quite tough if you have several controlls on your page that modify the output each in different ways.

Finally, this is from my point of view the most important reason for beginners. It comes with quite a progressive Build-chain, that helps you a lot in preventing bugs, if you knowto use it.

??HORIZONTAL
## Data-2-way-binding I

<input type="text" id="in" onkeyup="update()">
<div id="out" style="border:3px solid black; height:50px">


??HORIZONTAL
## Data-2-way-binding II

 ``` Html
<input type="text" id="in" onkeyup="update()">
<div id="out">
```

 ``` JavaScript
function update() {
    document.getElementById('out').innerHTML =
      document.getElementById('in').value
}
 ```

??HORIZONTAL

## Live-Reload-Server

??NOTES

Startup react app and show off  feature

??HORIZONTAL

## Test Framework

??NOTES

You alread know Jest. It gives you lots of features to mock classes and modules by overwriting require. It gives you a way to run your code. In case of Jest it runs on virtual-dom. Other frameworks use for example karmajs, which evaluates the code directly in the browser.

??HORIZONTAL

## Code Coverage

<img src="frameworks_overview/images/code-coverage-console.png">

??NOTES

Code Coverage gives you the possibility to see how much your tests cover your production code. It does that by instructing your code and without that you see it, it writes marker intoit befor and after each of your instructions. By that it can tell which of the lines of the production code had been called meanwhile a test run and give you such an overview as you can see here.
In this example, can see that the file calc.js seems to have a problem.

??HORIZONTAL

## Code Coverage

<img src="frameworks_overview/images/code-coverage-browser.png">

??NOTES

When you have a look into the report of the code-coverage, then you can even see, which line did not have called. Here we see that the function "sub" has not been called at all in the test. So it might be a good idea to do so. 

(Now show how to active code-coverage in jest and where to find the reports. Be careful, on startup project not all is shown.) 

??HORIZONTAL

## Babel Compilation

``` JavaScript

/******* ES6-Code *******/
const greeter = (name) => {
    return `Hello ${name}!`;
}

/************************
 * becomes compatible
 * with older browsers
 * ES5 code
 ************************/
"use strict";

var greeter = function greeter(name) {
  return "Hello ".concat(name);
};
```

??NOTES

show bable online

??HORIZONTAL

## Dependency Management I

``` JavaScript
const myLib = require('./my-lib') // This Code fails in the browser

myLib.doSomething();
```

??NOTES

I don't know if you ever recognized that, but if you try to run the javascript command require or import inside of a browsern it will fail.

??HORIZONTAL

## Dependency Management II

``` Html
<script src="./my-lib"></script>
<script>
  window.myLib.doSomething();
</script>

```

??NOTES

The old way of handling dependencies in Browsers were to call several script-Tags. But this has several drawbacks:

??HORIZONTAL

## Dependency Management III

* small files => long load time  <!-- .element: class="fragment" -->
* concatenated files => manually keep track of ordering  <!-- .element: class="fragment" -->
* optimize load time => minification  <!-- .element: class="fragment" -->
* .map-Files => deminify for debugging  <!-- .element: class="fragment" -->

??NOTES

Since you need to keep the complexity of the different files down, you create new files for every functionality. If you would load such small files, this would lead to a long loadtime at the client.
So there are tools to concatenate the different files. But if you do not take care in which order files are concatenated, your code would call something that is not yet defined. So you would need to order the files manually, which can be tidious in big projects. 
In addition, you don't want to provde the code as you have written it, because you probably created longer variable names and all that text needs to up lodaded to the user. Therefore there are tools to minify your code and for example rename your variables into shortcuts containing only 1 - 3 letters. This is less readable, but smarter for the performance.
If you need to read your code in production, you generate so called .map-Files that you only load if you have to debug your code.

??HORIZONTAL

## Dependency Management IV

This is what webpack and similar tools do.

??NOTES

Show code example

??HORIZONTAL

## History of Frameworks

* jquery   <!-- .element: class="fragment" -->
* AngularJS - the magic story...  <!-- .element: class="fragment" -->
* React - and its license  <!-- .element: class="fragment" -->
* Angular - the rais or fall?  <!-- .element: class="fragment" -->
* vue - a fork of angularjs  <!-- .element: class="fragment" -->

??NOTES
* (not to mention mootools, prototype.js, ember.js, knowckout.js, qooxdoo... )

??HORIZONTAL

## How to select a proper Framework

Consider

* License issues  <!-- .element: class="fragment" -->
* Performance / Loadsize  <!-- .element: class="fragment" -->
* Backwards Compatibility  <!-- .element: class="fragment" -->
* Maintenance / Support  <!-- .element: class="fragment" -->
* Popularity  <!-- .element: class="fragment" -->
* Team  <!-- .element: class="fragment" -->

??NOTES
When you decide for a framework you gain a a lot of functionality but you also bind longterm to that framework

??HORIZONTAL

## We want to use React because....

* it has a wide spread popularity:
* [stateofjs](https://2019.stateofjs.com/front-end-frameworks/)
* [Google Trends](https://trends.google.com/trends/explore?geo=US&q=react,angular,vue)

* it is easy to learn
* it supports FP
* it gives us the possibility to create a mobile native app

