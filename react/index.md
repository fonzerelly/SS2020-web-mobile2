# React

??HORIZONTAL

## Setup up a new react app

``` bash
npx create-react-app student-grading
cd student-grading
npm start
```

??NOTES

* npx is a tool being part of node. it allows you to run tools in your local installation or even install them first globally
* create-react-app will setup the whole react-app for you and even sets up a git repository and a test suite

??HORIZONTAL

<img src="react/images/new-react-app.png">

??NOTES

* "npm start" starts you a new web server that can be reached by localhost:3000.
* It will monitor your files and reload the page automatically when you change and save a file

??HORIZONTAL

## Testing

``` bash
npm test
```

??NOTES

Runs jest and evaluates your react tests each time the files changes.

??HORIZONTAL


## Build

``` bash
npm run build

...

File sizes after gzip:

  39.4 KB  build/static/js/2.2a42877b.chunk.js
  782 B    build/static/js/runtime-main.fef1349c.js
  657 B    build/static/js/main.b9631ac3.chunk.js
  547 B    build/static/css/main.5f361e03.chunk.css

```

??NOTES

* npm build creates a version of your code you could deploy. This should work for github-pages or similar but depending on the setup of your companies web-page it might need further hoops.

* can you tell me why the javascript files have such strange number in their filenames? why does the index.html not have such a number?

* html will be downloaded everytime the user calls the page and therefore is always up to date
* Javascripts files get cached, since the browser asumes they do not change so often. Therefore if you use javascript files with not changing names, your user might still have an old version running, when you already deployed a new version.
* The hashed numbers in the names of your js-files prevent that and force the browser to reload your js-files when you update your code.

??HORIZONTAL

## Take over controll

``` bash
npm run eject
```

??NOTES

* create-react-app sets up lot of default values for your project to simplify the startup as much as possible and giving you all those features we already seen
* but there will be a time, when those default values are not sufficient any more and you will want to modify those settings, that right now are hidden from you
* npm run eject will write out all those default-configs, so that you can modify them
* BUT! You can not revert eject. Afterwards, you will have to take care of the configs yourself. Even if a future version of a library expects a different setting of your configs.

??HORIZONTAL

## directory structure

* in public/index.html we have for example a test page of your app to run in...

??HORIZONTAL

## index.js

``` JavaScript
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```

??NOTES

So lets examine the entry point of our application
* ReactDOM.render is a method from the react library.
* It contains the App-jsx-tag. 
* What is JSX? Well it is a version of html that can be mixed with javascript in one file.
  This makes the application of the application logic to the markup more easy. We'll see that in more detail soon.
* In addtion we have this document.getElementById-call. this is vanilly javascript and would be the way we would apply javascript to the whole application if we would not have react
* it finds a div-node with the id "root" and renders the App-tag inside it. So this means
    a) you could rename the id of the root node to something else and 
    b) you could run several react apps / components in different parts of the page.


??HORIZONTAL

## App component
* remove everything from App Component
* be guided by error messages
* create AppComponent with header

??NOTES

So let's play around with our app a little:
First let us remove everything in App-Component, to learn what is needed for a react component
Now you see the Error message: "... You likely for got to export your component..."
So let us simply write "export default App"
This lead to the error App is not defined.
To define the component App we just need a function of the same name "function App () {}"
The new Error tells us that we need to return a value here: So let us return &gt;h1&lt;Student Grading&gt;/h1&lt;
Now we got told, that React needs to be imported to render html-tags.

So now we see a validly rendered h1-tag.
What we wee here is in fact no html. it is JSX - very similar to html but not examptly the same.


??HORIZONTAL

## Greet-Button
* Add button-tag to App Component and label it with Greet
* Create Greet-Function and apply onClick-handler to it.

??NOTES

let us create a button labled with greet and apply a function to it. Be aware that if you want to apply something javascripty into JSX-HTML, you need to wrap it in curly braces. So we write here a function greet with alert("Hallo Ansbach"). After applying it to onClick, we can evaluate it.

??HORIZONTAL

## Extract the Greet-Button

* comment out Greet-Button
* add &lt;Greet /&gt;-tag
* Follow errors to extract the greet component

??NOTES

No let us move the greet functionality to it's own file.
comment out the greet button and replace it with Greet-tag
Errors will guide you to creating Greet-Button
move also function there...


??HORIZONTAL

## Style App-component

* reset CSS
* style app.css

??NOTES

* set Background of App
* set height to 100vh
* box-siziing: border-box
* display: flex
* justify-content: space-around
* align-items: center


??HORIZONTAL

## Create Student-Component

* Setup hardcoded Student-Compnent
* style it

??NOTES

* border: 2px solid black
* width: 300px
* height: 300px
* background: white
* display: flex
* justify-content: space-around
* flex-direction: column
* align-items: center
* border-radius: 30px
* import styles

??HORIZONTAL

## Properties

``` JavaScript
function Student (props) {
  return (
    <div>
      <div>Name: {props.name}</div>
      <div>Matriculation: {props.matriculation}</div>
    </div>
  )
}
```

??NOTES

* write attributes name and matriculation to tag
* add props parameter to component fn
* console.log props
* replace hardcoded name and matriculation by props values
* refactor to deconstruction

??HORIZONTAL

## Grade-Component

* Create Grade Component 
* Add two buttons and span

??NOTES
Now here our plan is, create a component, that displays a grade and that can be increased and decreased.

??HORIZONTAL

## useState

``` JavaScript
import React, {useState} from 'react';

function Grade () {
  let [grade, setGrade] = useState(6);
}
```

??NOTES

Since we want something to change  the rendering of the component we need to create a special variable, that is known explicitly by react. To create such a variable we use the react function "useState". It expects the initial value of the variable and we get back a getter variable and a setter function to manipulate and read that variable in an array. To access it, we deconstruct the returned array.

??HORIZONTAL

## lets implement a inc/dec function

``` JavaScript
function Grade (...) {
  let [grade, setGrade] = useState(6);
  function inc () {
    setGrade(++grade)
  }
  function dec () {
    setGrade(--grade)
  }
  ...
}
```

??NOTES

By using the setter and getter methods, we can simply create an increment an ddecrement function.

If you now click on the buttons the value will change.

??HORIZONTAL

## Change Styling on state

create bem-css-classes for positive, normal, negative grades.

``` JavaScript
function format() {
  if (grade <= 2){
    return 'grade--positive'
  } else if (grade >= 5)
    return 'grade--negative'
  }
  return 'grade--normal'
}

... className={format()}
```

??HORIZONTAL

## Extend Student by Grade Component

??HORIZONTAL

## State in App

* create State students with more complex data structure.
* this will be replaced later by call to api
* replace several Students by mapping over state

``` JavaScript
  ...
  {students.map((student) => (
    <Student name={student.name} matriculation={student.matriculation}/>
  ))}
  ...
```
