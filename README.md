# Javascript core concepts 

## Introduction
Understanding some core concepts of Javascript.

### Syntax Parser
A program that reads your code and determines what it does and if its grammar is valid. The code you write isn't directly run on the computer, but there's that intermediate program between your code and your computer that translates your code into something the computer can understand. The JS engine on your browser does this. Reads your code and determines if it is valid. 

### Lexical Environment
Where something sits physically in the code you write.

### Execution Context
A wrapper to help manage the code that is running.
Two things are created by the JS engine: `Global Object` and `this`. In Execution Context `(Global) = Global object (window) = this`.

### Name/Value Pair
A name which maps to a unique value.

### Object
A collection of name value pairs.

### Global
Not inside a Function

### Execution Context is Created (Creation Phase) 
`Global object`, `this` and an `Outer Environment` are created. Setup Memory Space for Variables and Functions which is known as "Hoisting". Function in its entirety is placed into memory space, however the next phase (execution) is when the assigments are set. Puts a placeholder as `undefined` to `variables`.

### Javascript and undefined
First phase: `Global Oject`, `this`, `Outer Environment`, "Hoisting" variables setup (and set equal to 'undefined') and Functions Setup.
`undefined` is a special value that Javascript has with init that mean that variable has not been set.
If you don't set a variable name and try to call it you will get an uncaught reference error saying that the name is not defined. 

### ### Execution Context (Code Execution)
`Global object`, `this` and an `Outer Environment` already exist, and then the engine runs the code line by line, interpreting it and compiling it.

### ### Single Threaded, Synchronous exexution
Single threaded means that one command is executed at a time. Synchronous meaning one at a time in the order it appears.

### Function Invocation and The Execution Stack
Invocation means running a function or calling a function by using parenthesis ()
Execution Stack is one in top of the other in top of the other. Anytime you invoke a function, a new Execution Context is created and put on the Execution Stack, it will have its own space of functions and variables and will got through that creation space and execute line by line in the function. However if I have another function invocation its going to stop on that line on code an create another Execution Context and run that code.
Every function invocation creates a new Execution Context, creation phase and runs line by line.

### Variable Environment
Where the variables live and how they relate to each other in memory.

### The Scope Chain
Every Execution Context has a reference to its Outer Environment. When you ask for a variable while running a line of code in any particular execution context, if it can't find that variable it will look at the outer reference and go look for variables there somewhere down below it in the execution stack and that outer reference where that points is going to depend on where the function sits lexically.

### Scope
Is where a variable is available in your code and if it's truly the same variable or a new copy.

### let in ES6
Allow the Javascript engine to use the block scoping, so you can declare a variable and during the execution phase where its created, the variable is placed into memory and sets as undefined, however you will not be able to use it until the line of code is run during the execution phase that actually declares the variable. Its declared inside a block { }, its only available inside that block, true even for for loops.

### Aynchronous callbacks
Aynchronous means more than one at a time.
When we are talking about the JS Engine we need to know that are other engines and pieces of code like the Rendering Engine or the HTTP Request that run Javascript. The Javascript Engine  has hooks where it can talk to the rendering engine or request data, but all that is running async in the browser but in Javascript it runs synchronously.
The event Queue is a list that runs in the Javascript Engine, and this is full of notifications of events that are happening. When the browser somewhere outside the Javascript engine has an event that inside the Javascript Engine we want to notify of it gets placed on the Queue. The event Queue gets look only when the Execution Stack is empty. 

```JavaScript
/* example of an async callback, try clicking on the document when it loads and see what message comes first in the console.log*/

// long running function
function waitThreeSeconds() {
    var ms = 3000 + new Date().getTime();
    while (new Date() < ms){}
    console.log('finished function');
}

function clickHandler() {
    console.log('click event!');   
}

// listen for the click event
document.addEventListener('click', clickHandler);


waitThreeSeconds();
console.log('finished execution');
```

### Dynamic Typing
You don't tell the engine what type of data a variable holds, it figures it out while your code is running. Variables can hold different types of values because it's figured out during the execution.

### Primitive Type
A type of data that represents a single value. That is, not an object.

There are six primitive types:

	- `undefined`: represents lack of existence (you shouldn't set a variable to this, javascript engine uses and sets this value)
	- `null`: represents lack of existence (you can set a variable to this, javascript engine won't set this value ever)
	- `boolean`: true or false
	- `number`: floating point number (there's always some decimals).
	- `string`: a sequence of characters both '' and "" can be used
	- `symbol`:  used in ES6.

### Operators
A special function that is syntactically (written) differently. Generally, operators take two parameters and return one result. `(+, -, <, >, =.....)`

```JavaScript
prefix notation +3, 4
infix notation 3 + 4
postfix notation 3, 4+
```

### Operator Precedence
Which operator function gets called first. Functions are called in order of precedence. (Higher precedence wins). https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence

```JavaScript
var a = 3 + 5 * 4; // 23
//'*' operator has a higher precedence and son is called before the '+' operator function.
```

### Operator Associativity
What order operator functions get called in: left-to-right or right-to-left. When function have the same precedence.

```JavaScript
var a = 2, b = 3, c = 4;
a = b = c;
console.log(a) // 4 
console.log(b) // 4  
console.log(b) // 4
// Associativity is right-to-left
```

### Coercion
Converting a value from one type to another. This happens quite often in Javascript because it's dynamically typed.

```JavaScript
var a = 1 + '2';
console.log(a); // 12
// First parameter was coerced the Number 1 into string representation of 1.

console.log(1 < 2 < 3) // 1 < 2 = true; true < 3; 1 < 3; true
```

It isn't obvious when a type will be coerced. Special cases like undefined and null that won't coerce.
Equality operators will try to coerce values if their types are different. Strict equality operators will not try to coerce type operators.
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness

```JavaScript
// var a will be set as undefined in the creation phase,
// everything inside an if statement will try to coerce into a boolean. 
// undefined is coerced as false in boolean statement.
// when you ask if a value it will return a false when there's nothing assigned, unless it is a 0 Number.

var a;

if (a) {
    console.log('Something is there.');  
} else {
    console.log('Nothing is there.');     
} 

// "Nothing is there"
```

### Default Values
When you want to safely get a value when it is not defined use the `||` operator.

```JavaScript
function greet(name) {
     // creation phase name will be set as undefined
     name = name || 'My name'; // The OR operator will return the value that doesn't convert into false
     console.log('Hello ' + name);
}

greet(); // Hello My name
greet('Will') // Hello Will
```

### Objects and Functions
In Javascript Objects and Functions are very related. Objects have properties and methods. You think of an object as sitting in memory and then having references to other things sitting in memory that are connected to.
`[ ]` computer member access operator. bracket notation. only use if you need to change dynamically the property name.
`.` dot operator, associativity is left to right, so it looks first for object and then for the property or method.
`{}` is an object literal, a shorthand. The JS engine assumes you are creating an object. The syntax parser when executing sets in memory an object with properties and methods within.

```JavaScript
var person = new Object(); 
var person = {}; // an object literal, a shorthand. The JS engine assumes you are creating an object.

person['firstname'] = 'William' // [ ] computer member access operator. bracket notation. only use if you need to change dynamically the property name.
person.firstname = 'William' // dot operator, associativity is left to right, so it looks first for object and then for the property or method.
```

### Object Literals and JSON
Json JavaScript Object Notation, it looks a look like Javascript literal notation it is inspired but it is not exact the same. In Json, properties must be wrapped in quotes, and will only accept double quotes. Json has stricter rules.

```JavaScript
var objectLiteral = {
  firstname: 'Mary',
  isAProgrammer: true
}

console.log(JSON.stringify(objectLiteral)); // {"firstname":"Mary","isAProgrammer":true}
var jsonValue = JSON.parse('{ "firstname": "Mary", "isAprogrammer": true}');
console.log(jsonValue); // Object {firstname: "Mary", isAprogrammer: true}
```

## Function and Objects

### First Class Functions
Means that in the programming languange everything you can do with other types you can do with functions, assign them to variables, pass them around, create them on the fly.

### Function
Like any object it resides in memory, it is a special type of object because it has all the features of a normal object and has some other special properties. You can attach properties and methods to a function because it is just an object.
Function object has some hidden special properties: 

	1. Name, it is optional, it can be anounymous.
	2. Code, where the actual lines of code written set. It is invocable ().

```JavaScript
function greet() {
     console.log('hi');
}

greet.language = 'english';
console.log(greet.language); // "english"
// since function is basically an object, you can attach properties to it and then call them.
```

### Function Statements and Function Expressions

`Expression` is a unit of code that results in a value. It doesn't have to save to a variable.
`Statement` just does work.

```JavaScript
var a;
a = 3 // 3 
1 + 2 // 3
// the return or result in both cases is an expression because it returns a value.
```

`function statement`, it means that doesn't return anything. When function is running in the execution phase it doesn't do anything, it keeps going.
`function expression`. We are creating an object on the fly, and setting it equal to the variable, and that variable is set in memory. When this line is executed it results in an object being created, and it returns an object essencially.

```JavaScript
/*invokes the code. it can be invoked before the creation line since it is a function and everything that's inside it is set in memory. */
greet() // "hi"

/* function statement, it means that doesn't return anything */
function greet() {
     console.log('hi');
}

/* function expression. We are creating an object on the fly, and setting it equal to the variable, and that variable is set in memory. */
var anonymousGreet = function() {
     console.log('hi');
}

/* invokes the code. it should be invoked after the creation line since it is a variable and in the creation phase it is set in memory as undefined. */
anonymousGreet() // "hi"

/* function expression that is passing a function as a paramater to another function and then use it. First Class function Functional programming.
function log(a) {
     a();
}

log(function() {
     console.log('hi');
});
```

### By Value VS By Reference & mutate
`By Value`: passing or referencing one value as primitive type to another by copying the value , they become the same by copying the value into two separate spots in memory. They are copies of each other sitting in two spots in memory.
`By Reference`: points to the same location in memory, so when you mutate the value of an object it will also change in the other one that is referencing to.
`mutate`: to change something, inmutable: it can't be changed

```JavaScript
// by value (primitives)
var a = 3;
var b;

b = a;
a = 2;
console.log(a); // 2
console.log(b); // 3

// by reference (all objects (including functions))
var c = { greeting: 'hi' };
var d;

d = c;
c.greeting = 'hello'; // mutate

console.log(c); // Object { greeting: 'hello'}
console.log(d); // Object { greeting: 'hello'}

// by reference (even as parameters)
function changeGreeting(obj) {
     obj.greeting = 'Hola' // mutate
}

changeGreeting(d);
console.log(c); // Object { greeting: 'Hola'}
console.log(d); // Object { greeting: 'Hola'}

// equals operator sets up new memory space (new address)
c = { greeting: 'howdy'}
console.log(c); // Object { greeting: 'howdy'}
console.log(d); // Object { greeting: 'Hola'}
```

### Objects, Functions and 'this'
When a function is invoked, a new execution context is created and put on the execution stack, that determines how the run is executed, so think of execution context as focusing on that code portion. Each execution context has its variable enviroment and has a reference to  its outer enviroment where it sits physically in the code, which tells you how to look down the scope chain.
The JS engine gives us the 'this' variable each time the execution context is created (a function is run). this will be pointing at different at different objects or things depending on how the function is invoked.

```JavaScript
console.log(this) // Window

function a() {     
     console.log(this);
     this.newVariable = 'hello';
}

/* the this keyword will be pointing the global object if I invoke the function in the global enviroment */
a(); // Window
console.log(newVariable) // 'hello'

var c = {
     name: 'The c object',
     log: function() {
          var self = this; //safely points the same location in memory.
          this.name = 'Updated c object';
          console.log(this); 
          
          var setname = function(newname) {
              this.name = newname; 
          }
          setname('Updated again! The c object!'); // the name var is created in the global object and not in the c object.
          console.log(this); // Object {name: "Updated c object", log: function}
     }
}

c.log(); // Object {name: "Updated c object", log: function}
```

### Arrays, Collections of Anything
An array is a collection and can hold many things. Since JS is dynamically typed it can collect whatever I want.

```JavaScript
var arr = [
     1,
     false,
     {
          name: 'Will',
          address: '111 Main St.'
     },
     function(name) {
          var greeting = 'Hello ';
          console.log(greeting + name);
     }
];

arr[3](arr[2].name); // 'Hello Will'
```

### Arguments and Spread
When you execute a function arguments is a special keyword that javascript sets up automatically.
Arguments are the parameters you pass to a function. Javascript gives you a keyword of that same name which contains them all.

```JavaScript
function greet(firstname, lastname, language) {

    language = language || 'en';

    if (arguments.length === 0) {
        console.log('Missing parameters!');
        console.log('-------------');
        return;
    }

    console.log(firstname);
    console.log(lastname);
    console.log(language);
    console.log(arguments);
    console.log('arg 0: ' + arguments[0]);
    console.log('-------------');

}

greet(); // 'Missing parameters -------
greet('John'); // John undefined en ["John"] arg 0: John ----
greet('John', 'Doe');  // John Doe en ["John"] arg 0: John ----
greet('John', 'Doe', 'es'); // John Doe es ["John"] arg 0: John ----

// in ES6 I can do:  function greet(firstname, ...other)
// and 'other' will be an array that contains the rest of the arguments
```

### Automatic Semicolon insertion
The syntax parser inserts semicolon where it is expecting one. For some particular statements it will put for you and can break the code. You should always write semicolons.

```JavaScript
function getPerson () {
     return 
     {
          firstname: 'Will'
     }
}

console.log(getPerson()); // undefined
// The JS engine automatically inserted a semicolon after the return statement, meaning it quit out of the function.
```

### Whitespace
Invisible characters that create literal "space" in your written code, carriage returns, tabs, spaces.

### IIFFe Inmediately Invoked Function Expression
You can safely create variables without colliding with another same name variables since those are created on a different execution context

### Closures
A feature of the Javascript language .
When the code of a function inside another function is invoked, it goes up the scope chain to its outer lexical environment to look for a variable that does not exist inside that inner function. An inner function will have a reference to its outer environment even though the execution of the outer enviroment is cleared out.
It doesn't matter when we invoke a function or its outer enviroment is still running, it will always have access to the variables it should have access to.

```JavaScript
function greet(whattosay) {
     return function(name) {
         console.log(whattosay + ' '  + name);
     }
}
var sayHi = greet('Hi');
sayHi('Will'); // "Hi Will"
```

### Function Factory making advantage of Closures
Since the function makeGreeting each time is invoked, it creates a new execution context, in this case one with language parameter as 'en' and the other as 'es' those variables are stored in memory and when you invoke the inner function of each invoked function, you will still have access to the variables outside, in this case the language.

```JavaScript
function makeGreeting(language) {
    return function(firstname, lastname) {
        if (language === 'en') {
            console.log('Hello ' + firstname + ' ' + lastname);   
        }
        if (language === 'es') {
            console.log('Hola ' + firstname + ' ' + lastname);   
        }
    }
}

var greetEnglish = makeGreeting('en');
var greetSpanish = makeGreeting('es');

greetEnglish('John', 'Doe');
greetSpanish('John', 'Doe');
```

### Callback Function
A function you give to another function, to be run when the ohter function is finished, so the function you invoke 'calls back' by calling the function you gave it when it finishes.

```JavaScript
function tellMeWhenDone(callback) {
     var a = 1000;
     var b = 2000;
     callback();
}

tellMeWhenDone(function() {
     console.log('I am done');
});
```

### Call() Apply() Bind()
On each execution context we have a variable enviroment, outer enviroment and 'this'. This keyword can point the global object sometimes or can point the object that contains the function if the function is a method attach to an object. To be able to control what the this variable ends up meaining when the execution context is created.  All functions are objects and have access to methods call, apply bind.

Bind() creates copy of whatever function calling, and whatever object you pass to this method, its what this variable points to by reference:
Apply and Call invokes the function setting extra parameters, call as strings, apply as array.

```JavaScript
var person = {
  firstname: 'Will',
  lastname: 'Doe',
  getFullName: function() {
    var fullname = this.firstname + ' ' + this.lastname;
    return fullname;
  }
}

var logName = function(lang1, lang2){
  console.log('Logged: ' + this.getFullName());
  console.log('Arguments: ' + lang1 + ' ' + lang2);
  console.log('------------');
}

//creates new copy
var logPersonName = logName.bind(person);
logPersonName('en');

//call will execute the function first parameter is this, and then pass pararameters
logName.call(person, 'en', 'es');

//call will execute the function first parameter is this, and then pass array of params
logName.apply(person, ['en', 'es']);

//function borrowing
var person2 = {
  firstname: 'Jane',
  lastname: 'Doe'
}

console.log(person.getFullName.apply(person2)); // Jane Doe

// function currying
function multiply (a, b) {
  return a*b;
}

//giving a permanent value
var multypleByTwo = multiply.bind(this, 2);
multypleByTwo(3) //6
```

### Function Currying
Creating a copy of a function but with some preset parameters. Very useful in mathematical situations.

### Functional Programming
Having first class functions we can apply functional programming. Whe think and code in ways of function.

```JavaScript
function mapForEach(arr, fn) {
  var newArr = [];
  for (var i = 0; i < arr.length; i++) {
    newArr.push(
      fn(arr[i])
    )
  }
  return newArr;
}

var arr1 = [1, 2, 3];
console.log(arr1); //[1, 2, 3]

var arr2 = mapForEach(arr1, function(item){
  return item * 2;
});

console.log(arr2); //[2, 4, 6]

var arr3 = mapForEach(arr1, function(item) {
  return item > 2;
});
console.log(arr3); //[false, false, true]

var checkPastLimit = function(limiter, item) {
  return item > limiter;
}

var arr4 = mapForEach(arr1, checkPastLimit.bind(this, 1));
console.log(arr4); //[false, true, true]

var checkPastLImitSimplified = function(limiter) {
  return function(limiter, item) {
    return item > limiter;
  }.bind(this, limiter);
}

var arr5 = mapForEach(arr1, checkPastLImitSimplified(2));
console.log(arr5); //[false, false, true]
```

## Object-oriented Javascript and prototypical inheritance

### Inheritance:
One object gets access to the properties and methods of another object.

### Prototype
All objects (including functions) have a prototype property. A property that is a reference to another object. proto {}. This object has other objects. The prototype can be chained to another prototype and so on. So when I try to look for obj.prop2, if JS doesn't find it in the main object it will look for the property in it's prototype, and so on. And that's called the Prototype Chain, when you have access to properties or methods in a secuence of objects.
If I have another object "obj2", it can point to the same object in it's prototype. Calling obj2.prop2 will return the same exact property in memory than obj.prop2.

```JavaScript
var person = {
  firstname: 'Default',
  lastname: 'Default',
  getFullName: function() {
    return this.firstname + ' ' + this.lastname;
  }
}

var john = {
  firstname: 'John',
  lastname: 'Doe'
}

//don't do this ever
john.__proto__ = person;
console.log(john.getFullName()); //John Doe
console.log(john.firstname) //John (first looks at the top of the chain)
```

### Everything is an object (or a primitive)
Functions, arrays and basic objects all have a prototype, except one thing, the base object in javascript.

```JavaScript
var a = {};
var b = function() {};
var c = [];

a__proto__ //Object {} //the very bottom of the prototype chain
b__proto__ //function Empty() {}
c.__proto__ //[]
```

### Reflection
An object can look at itself, listing and changing its properties and methods.

```JavaScript
// continue from previous example

for (var prop in john) {
     console.log(prop + ': ' + john[prop]); // reachs out every property on the object and object's prototype
     if (john.hasOwnProperty(prop)) {
          console.log(prop + ': ' + john[prop]); // reachs out every property on the object only          
     }
}
```

### Function Constructors 'new' and the history of javascript
Brandon Ike designed Javascript for marketing purposes, trying to bring Java developers to work inside JS. One of the element of this marketing strategy was the 'new' and a Class. A Class in Java is not an object but it defines that object, and use the new keyword to create the object from that Class. JS doesn't have classes per se, but needed a way to be able to create objects with that kind of syntax.

```JavaScript
function Person(firstname, lastname) {
  console.log(this) //Person {}
  this.firstname = firstname;
  this.lastname = lastname;
}

var john = new Person('John', 'Doe');
console.log(john); //Person {  firstname: "John", lastname: "Doe" }
// the new creates an empty object and the this.firstname and this.lastname is now pointing to that empty object.
```

The new keyword is an operator. When we say new, inmediately an empty object is created, and then it invokes the function. when the function is called we know that execution context generates for us a variable called 'this'. In the case where you use the keyword new, it changes to where the variable this points to and that's what's returned.

### Function Constructors
A normal function that is used to construct objects. The 'this' variable points a new empty object, and that object is returned from the function automatically.

### Setting the prototype in function constructors
When you use a function constructor, it already set the prototype for you. Function is an object, it can have a name, it has code which is invocable, and all functions has its prototype created as an empty object but it is never used unless you use the new keyword. The prototype is not the prototype of the function, it is the prototype of any objects created if your using the function as a constructor.
All functions get the prototype property, its starts its life as an empty object and you can addon to it. The prototype chain is that every object has this special property that points to another object that is its prototype so it looks for properties and methods down that chain. When you call the new keyword it creates an empty object and sets the prototype of that empty object to the prototype property of the function you then called. Every objects you create using this function constructor means that the object thererfore created has a prototype and properties and methods.

```JavaScript
Person.prototype.getFullName = function() {
  return this.firstname + ' ' + this.lastname;
}
```

In good code properties are set inside the function, and methods in the prototype. Functions are objects and take up memory space, so every time you add a function inside the function it means that every object has its own copy of that function, but if it is set to the prototype you will only have one. 


-----

### Strict Mode
Allows to play a program or a function in a strict operating context, it makes debugging easier. This alerts problem in your code. It is a string. 

```JavaScript
// Using a variable undeclerared causes an error:
myNumber = 1; // error in strict mode

// Stops you from using words that are reserved for future javascripts:
var let = 1; // error

// You can't delete functions, variables or function arguments in strict mode:
var foor = 1;
delete foo; // error

// Makes eval keyword safer.
```

### NaN
The correct way to to know if something is NaN is by comparing if NaN is NaN.
Since NaN is the only javascript value that is treated unequal to itself then and only then, it will be actually NaN.

```JavaScript
NaN === NaN // false
```

### CORS 
Stands for Cross Origin Resource sharing. Allows you tu break the same origin policiy of a browser.
The Origin header is always sent by the browser on a CORS request.
The Acesss-Control-Allow-Origin header needs the be present on a CORS response to a GET request for the browser to allow a request to pass through.
If we were making a POST CORS request, the OPTIONS HTTP request the browser sends first.
Access-Control-Request-Method would be an acceptable response for the browser to allow the POST request


### JSONP
It is a solution for the same-origin policy. It was created to retrieve from different domain. It only works with GET request. You get a response as a function.


-----

### DOM

DOM stands for Document Object Model. It is a JavaScript representation of the content of a webpage. It is a bunch of objects representing all the HTML and CSS of the webpage that you can interact with via JS. Each node inside the webpage gets converted by the browser into ojects, each with their own properties and methods, and they are assembled into a tree with different branches, each tree has a top piece which is called the root of the tree.


### Methods to select the DOM

getElementById, getElementsByTagName, getElementsByClassName, querySelector, querySelectorAll

```JavaScript
document.getElementById('id') // returns an oject with the same ID
document.getElementsByTagName('tag') // returns a full collection of types of elements selected
document.getElementsByClassName('class') // returns a collection of elements that contains the selected class
document.querySelector(el) // returns a single element that is passed in a CSS selector
document.querySelectorAll(el) // returns a collection of elements that are passed in a CSS selector
```

### Methods to manipulate the DOM

classList, getAttribute(), setAttribute(), appendChild(), append(), prepend(), removeChild(), remove(), createElement, innerText, textContent, innnerHTML, value, parentElement, children, nextSibling, previousSibling, style,

 ```JavaScript
document.querySelector('h1').innerText // returns all the text in between the tags.
document.querySelector('h1').innerText = 'new text' // sets new text inside the selected element.
document.querySelector('h1').classList // returns a collection of classes contained inside the element.
document.querySelector('h1').classList.add('new-class') // adds class to the collection inside the element.
```

### DOM events



### Event Bubbling & Event Capturing

When you click on something, it's actually two phases that that event travels to. The first phase is the Capturing phase where the event travels from the root to the target (button), the second phase is the Bubbling phase in which the event travels back from the target to the root again. You can add event listeners that listen to that phases independently, the last parameter is a boolean, and if set true it listens for events on the capturing phase, if set to false it listens to the bubbling phase, as default is set to false (bubbling).

```JavaScript
var items = document.querySelectorAll('.item');
items.forEach(function(item){
  item.addEventListener('click', function (event) {
    console.log(item.classList[0]);
  }, true);
});
```

### stopPropagation() & preventDefault()

stopPropagation actually stops the event from either presiding down the capturing phase or going up the event bubbling phase and no listeners will be called after the event has called to stop propagating.

preventDefault stops the default behavior that that event would have triggered in whatever element you performed the event on (link, checkbox, etc).


