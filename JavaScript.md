# Prototypes

set prototype use `__proto__`

## Prototype Property

new F() creates new object
    object's `[[Prototype]]` is set to `F.prototype`

if `F` has a `prototype` property == Object type
    then new operator uses it to set `[[Prototype]]` property

`F.prototype` means a reqular property named `"prototype"` on `F`
    e.g. `Rabbit.prototype = animal` => When a `new Rabbit` is created, assign its `[[Prototype]]` to `animal`

    inheritance of `rabbit` from `animal`

## Default F.prototype, constructor property

every function has `prototype` property
    even if not supplied

default `"prototype"` is object with only property construtor that points back to function itself

can use `constructor` propertry to create new object usering same constructor as the existing one

```js
function Rabbit(name) {
  this.name = name;
  alert(name);
}

let rabbit = new Rabbit("White Rabbit");

let rabbit2 = new rabbit.constructor("Black Rabbit");

```
can add/remove props to default "prototype" instead of overwriting as a whole

# Closures

combination of function and lexical environment from which it was declared

allows function to access variables from an enclosing scope
    even after it leaves scope it was declared in

can refter to outer scope variables even after function has returned

allows for data encapsulation
    some data not directly exposed

# Event Loop

## Call Stack

js single threaded
    run one piece code at a time

call stack: data structure that records where we are in a function
    call: push onto stack
    return: pop off of stack

blocking
    code that is slow on the stack are blocking

can't do anything while blocked because single threaded
    solution: asynchronous callbacks

## Concurrency and the Event Loop

concurrency can happen because webapis
    
    pushes call back onto taskqueue

if stack is empty, event loop pushes callback from task queue to call stack

## Callbacks

can be a function that another function calls

or 

one that will be pushed on callback queue

dont want to fill callback queue with slow code or else won't be able to rerender quickly

#IIFE

immediately called after you define it

when you want to creat a new variable scope

surrounding parenthesis prevent from treating as a function declaration

final parens execute the function

calling function exactly when you are defining it

attach private data to a function
creates fresh environments
avoids polluting the global namespace

# Type Checking

== checks for equality with coercion

=== checks for equality without coersion
    strict equality

when comparing a boolean to something other than a boolean
    JS coerces boolean to a number and compares

number and string - string -> number

# this

methods: functions stored in object properties

methods allow objects to act
    reference the object as `this`

`this` defined at run time

when a function declared, it may use `this`
    `this` has no value until function is called

function can be copied between objects 

when a function is called in the method syntax
    `this` value === object

arrow functions have no this

# Hoisting

moving var and function declarations to the top of their respective scopes during compilation phase

function declarations = completely hoisted
    can be called before it is defined

vars partially hoisted
    var declarations are hoisted but not assignments

# `new` Keyword

constructor functions

creates a new object

sets the object's prototype to be the prototype of the constructor function

executes the contructor function with `this` as the newly created object

returns the created object
    if constructor returns an object, object is returned

# Event Bubbling

when an event happens on an element, it first runs the handlers on it, then on its parent, then all the way up on other ancestors

almost all events bubble
    focus event does not bubble

## event.target

handler on parent el can always ge the details about where it actually happened

most deeply nested el that caused the event is called a target element, accessible as event.target

event.target is the target element taht initiated the event
    doesn't change through the bubbling process

`this` is the current element, the one that has acurrently running handler on it

`this`(event.currentTarget) is the clicked on form because the handle runs on it

event.target is the concrete element isnide the form that actually was clicked

## Stopping Bubbling

bubbling event goes from the target element straight up
    normally till <html> and then document object and some events event reach window

event.stopPropagation() will decide that the event has gone far enough

don't stop bubbling without real need

## Capturing

another phase of event processing

rarely used, but can be useful

DOM Events descrbe 3 phases of event propagation:
    capturing phase: event goes down to the el

    Target phase: the event reached the target element

    Bubbling phase: the event bubbles up from the element

event foes through thr ancestors chain down to the element(capturing)
    then reahes the target

    then goes up(bubbling)

handlers added using on<event> property or using HTML attributes or useing addEventListener(event, handler) only run on 2nd and 3rd phase

to catch an event on capturing phase, add 3rd arg to addEventListener to true
    false(default): handler is set on the bubbling phase

    true: handler is set on the capturing phase

event.eventPhase that tells us the number us the number of the phase on which the event was caught

# Event Delegation

event delegation -> capturing and bubbling allow us to implement on eof the most powerful event handling pattern

`event.target` to focus on specific element

put single handle on the container

in he handle - check the source of element `event.target`

if event happened inside an element that interests us, handle the event

simplifies initialization and saves memory
    no need to add many handlers

less code
    when adding or removing elements, no need to add/remove handlers

DOM modifications
    we can mass add/remove elements with `innerHTML` and alike

has limitations
    event must be bubbling
        some events do not bubble
        
        low level handlers should not use `event.stopPropagation()`

    delegation may add CPU load
        container-level handler reacts on events in any place of the container
            no matter if they interest us or not

            usually load is negligible, though

# ES5 vs ES6

ES6 features:
    syntactic sugar(class)
    JS enhances(import)
    fix some bad parts of JS (let)

## Block Scope

ES5 only had function level scope
    wrap code in functions to create scope

ES6 proviseds block level scoping
    curly braces to scope

    when we use let or const instead of var

### Prevent Variable Hoisting Outside of Scope

### Prevent Duplicate Variable Declaration

ES6 deosn't allow duplicate declaration of variables with let or const in the same scope

### Eliminates the Need for IIFE

in ES5 had to use IIFE
    ensure no pollution or overwriting of the global scope

ES6 just use curly braces and const or let

### babel

a tool to convert ES6 to ES5

### Trivial to Use Functions In Loops

ES5 if function in loop
    if that function tried to access the looping variable, `i`

    bc of hoisting there would be an issue

ES6 use let

## Lexical "this"

in ES5, `this` can vary based on how and where it is called

ES6 fixes with lexical `this`

ES6 uses simple fat arrow function and lexical this is created

## Arguments

es5, args acts like an array, but it isn't an  array
    so array functions not available

ES6, Rest parameters
    `...args` is an array so can use array functions

## Classes

no such this as "Class" in JS
    people have treated the function that creates objects as classes
        function constructors

Since JS doens't support "Classes"
    just simulates via prototypes

    syntax has been very confusing

    esp when creating subclasses, calling functions on parent classes, etc

ES6 brings class

## Strict Mode

`"use strict"`

helps identify common issues and securing JS

ES5 strict mode optional

needed in ES6 for many features

# Error Handling

usually script dies in case of an error

`try...catch` allows us to catch errors and do something

## Try and Catch

2 blocks: `try` and `catch`

```js
try {

  // code...

} catch (err) {

  // error handling

}
```
first try is executed 

if no errors, catch ignored

if errors, try is stopped
    control flows to the beginning of catch

    err contains error object with info

`try...catch` only works for runtime errors
    needs to be valid JS

    only errors that occur in valid code

    also called exceptions

`try...catch` works synchronously

## Error Object

built in errors have 
    name: error name

    message: textual message about error details

    stack: current call stack; a string with info about the sequence of nexted ccalls that led to the error

## Throwing Our Own Errors

### throw operator

generates an error

`throw <error object>`
anything can be used as error obj
    better to use objects
    preferably with name and message properties

can use built in error constructors to create error objects

## Rethrowing

`try...catch` meant to catch incorrect data
    catch gets all errors from try

catch should only process errors that it knows and 'rethrows' all others
    catch gets all errors

    in catch block analyze the object err

    if we don't know how to handle it, throw err

## Try, Catch, Finally

if finally clause exists
    runs in all cases
    after try if no errors
    after catch if errors

finally clause works for any exit from `try...catch`
    includes explicit return

`try...finally` useful
    apply it when we don't want to hanlde errors right herre

    want to be sure that process we started are finalized

## Global Catch
```js
window.onerror =function(message, url, line, col, error) {

};
```
send the error message to developers

# Event Reference

DOM events sent to noticy code of interesting things that have taken place

can represent basic user interactions to automated notifications of things happening in the rendered model

## Page Lifecycle

DOMContentLoaded - browser fully loaded HTML and DOM tree is built
    external resources may not be loaded
        pics
        style sheets
    
    Dom is ready so handler can look up DOM nodes, initialize interface

load - browser loaded all resources
    additional resources loaded

    get image sizes

beforeunload/unload - when user leaves page
    check if user saved the changes and aske them whether they really want to leave

### DOMContentLoaded

happens on the document object

must use `addEventListener` to catch it

#### Scripts

when HTML runs into a `<script>` in the text
    can't continue building the DOM

    must execute script immediately

DOMContentLoaded may only happen after all such scripts are executed

external scripts also put DOM buildeing to pause

only exception:
    scripts with async and defer attributes

    they tell the browser to continue processing without waiting for the scripts

    lets user see the page before sciprts finish loading
        good for performance

#### Scripts with async and defer

only work for external scripts
    ignored if no src

tell the browser that it may go on working with the page
    load the scrip in background

    run the script when it loads

    script doesn't block DOM buildeing and page rendering

##### Order

scripts with async execute in the load first order
    their document order doesn't matter

    whatever loads first runs first

scripts with defer always esecute in the document order

##### DOMContentLoaded

scripts with async
    load and execute while the doc has no yet been fully downloaded

    happens if scripts are small or cached and doc is long enough

scripts with defer 
    execute after the doc is loaded and parsed

    right before DOMContentLoaded

async used for independent scripts like counters or ads
    don't need acces to page content

defer used for scripts that need DOM and/or their relative execution order is important

#### styles

external style sheets don't affect DOM
    DOMContentLoaded does not wait for them

if we have script after style
    script must wait for the sytlesheet to execute

script may want coordinates and other style-dependent properties of els
    so has to wait

as DOMContentLoaded waits for scripts, it now waits for styles before them as well

#### Built in Browser Autofill

Firefox, Chrome, and Opera autofill forms on DOMContentLoaded
    username, password

if DOMContentLoaded is postponed by long-loading scripts
    autofill also awaits

### window.onload

load event on the window obj triggers when the whole page is loaded
    including style, images, and other resources

### window.onunload

when visitor leaves the page

do something there taht doesn't involve delay
    closing related popup windows

    can't cancel the transition to another page

### window.onbeforeunload

if visitor initiated navigation away from the page or tries to close the window
    beforeunload handler asks for additional confirmation

### readyState

document.readyState gives us info
    "loading"- doc is loading
    "interactive" - doc was fully read
    "complete" - doc fully read and all resources loaded

can check document.readyState and set up a handler or execute the code immediately if it's ready

readystatechange event that triggers when the state changes

    alternative mechanics of tracking the doc loading state

    rarely used

# Variables

var only option before ES6

vars and funcs declared inside another function cannot be accessed by any of the enclosing scopes
    function scoped

vars declared inside a block-scope can be accessed from outsidfer of the opening and closing curly braces of block
    if statements and for loops

undeclared variable w/o var, let or const
    creates var variable in global scope

let and const not hoisted, block scoped

const cannot be reassigned
    props can be changed

# Strict Mode

"use strict"
    at beginning of script or function

global if declared at beginning of script

inside function
    has local scope

not statement, expression

indicate that the code should be executed in strict mode

connot use undeclared variables

## Purpose

makes it easier to write secure JS
    bad syntax => real errors

    mistyping variable name creates new global variable 
        in strict, throw error

# Rest and Spread

many JS functions suppor tan arbitrary number of args

## Rest Parameters

`...`

fucntion can be called with any number of arguments
    only defined ones will be counted

rest params can be mentioned in a cuntion definition with `...`
    gather the remaining params into an array

must be at the end
    last variable in function definition

## The Arguments Variable

special array like obj named arguments
    contains all arguments by their index

in older versions, only way to get all the args of the function, no matter the #

array-like and iterable, but not an array
    doesn't support array methods

always contains all args
    can't capture them partially, like with rest parameters

arrow functions doen't have "arguments"
    take from outer "normal" function

## Spread Operator

parameters => array

`...arr` expands an iterable object arr into the list of args

can pass multiple iterables

combine with normal values

used to merge arrays

turn string into array of chars
    could also use `Array.from(str)

internally uses iterators to gather els, same way `for..of` does

# Bind

lose `this` with object methods and passing object methods along

## Losing this

once method is passed elsewhere seperately from obj 
    this is lost

    lose conext method defined in

## Solution 1: Wrapper

a wrapping function

receives user from outer lexical environment and then calls the method normally

if obj changes value, it will call the wrong obj

## Solution 2: Bind

`func.bind(context)`

function fixed to this

```js
let user = {
  firstName: "John"
};

function func() {
  alert(this.firstName);
}

let funcUser = func.bind(user);
funcUser(); // John
```

# Function Object

functions are objects

callable action objects

## Name Property

contain a few usable properties
    name is the name property

function.name

## Length Property

returns number of function parameters

rest parameters not counted

used for introspection in functions that create other functions

## Custom Properties

add props of our own

property is not a variable

## Named Function Expressions

NFE
    function expressions that have names

allows the function to reference itself internally

is not visible outside of the function

function name may change, this ensures that won't affect this

# Function Expression vs. Declaration

function expression is created when execution reaches it 
    usable from then if not hoisted

function declaration
    can be called before and after defined
    
    hoisted

# Value vs. Reference

primitives assigned by value
    null
    undefined
    boolean
    number
    string
    symbol

compound values always create a copy of the reference on assignment
    objects
    arrays
    funciongs

to copy a compound value by value, you need to make a copy of it
    ref does not point to original value

# Types & Coersion

7 types:
    null
    undefined
    boolean 
    number 
    string 
    object
    symbol

all primitives except for object

undefined = absence of definition
    default val for uninitialized vars, func args not provided, missing props of objs

    funcs return undefined when nothing returned explicitly

null = absence of value
    assignment value to a var

    represents no value

Falsy values
    ""
    0
    null
    undefined
    NaN
    false

anything not falsy is truthy
    boolean coerced to true

    empty arrays, objs, and func = true

## String and Number Coersion

`+` for both number addition and string concatentation

`*`, `/`, `-` exclusively for numberic operations
    forces strings to be coerced into a number

# Prototypal Inheritance

classical inheritance:
    objs inherit from classes

    like blueprint or desc of the obj to be created

    via constructor functions using new keyword

    downsides:
        inflexible hierarchy

        tight coupling problems

        fragile base class problems

        duplication problems

        gorilla/banana problem

protypal inheritance
    inherit directly from other objs

    `Object.create()`

Prototype delegation
    an obj used as a model for another obj

    new obj gets a ref to the prototype and its properties
        `Object.create()`

Concatenative inheritance
    inheriting properties from one obj to another by copying the obj's prototype properties

    without retaining the ref between them
        `Object.assign()`

Functional inheritance
    uses factory function
        function not a class or constructor that returns an object without using the new keyword

    create obj then adds new props directly to the created obj

    allows data encapsulation via closure

## Favor Composition over class inheritance

class inheritance ought to be avoided

design your type regarding what they are
    makes strict pattern

composition design types regarding what they do
    more flexible and reusable

# Global Object

provides all global variables and functions

multiple in browser scripts would use that obj and share variables through it

`window` in browser
    in Node.js `global`

provides access to built-in functions and values
    defined by the specification and env

    can call `alert` directly or as a method of `window`

provides acces to global function declarations and var variables
    does not have variables declared with `let/const`

## Uses of Window

in-browser, `window` sometimes used
    incredibly rare server side like in node

useful to access global var if func has local one with same name

check if certain global variable or built-in exists

take variable from the right window
    browser may open multiple windows and tabs

    allows windows that come from the same site to access variables from one another

## This and Global Object

`this` occasionally global obj

in browser, `this` === window

when function with `this` is called in non-strict mode, it gets the global object as this

# Promise

producing code 
    does something that takes time

consuming code
    wants result of producing code

promise
    JS object that links producing code and consuming code

has many internal properties
    state
        initially pending

        changes to fulfilled or rejected

    result 
        arbitrary value of your choice

        initially undefined

calls function that it takes as args
    resolve(value)
        job finished successfully

        sets state to fulfilled

        sets result to value

    reject(error)
        indicate that error occured

        sets state to rejected

        sets result to error

executor should do a job then call resolve or reject to change the state of the corresponding Promise object

can only be a single result or error
    further calls of resolve and reject ignored

    resolve/reject expect one arg

## Consumers: 'then' and 'catch'

consumers registered through 'then
 and 'catch'

syntax of then:

```js
promise.then(
    function(result) { /* handle a successful result */ },
    function(error) { /* handle an error */ }
);
```
first arg is func that
    runs when promise resolved

    receives result

second arg
    runs when Prom rejected

    recevies the error

if only interested in errors
    use catch

    analog of `.then(null, f)`

on settled promises, then runs immediately

always async

## Promise Chaining

`promise.then` returns a promise so can call then on it

normally value returned by .then immediately passed to next handler

exception:
    if returned value === promise
        further execution is suspended until it settles

allows for chaining of async actions

grow down not in a pyramid shape

Thenables
    .then may return a thenable obj and will be treated same as promise

fetch gets info from remote server
    returns promise

    resolves with a response obj when remote server respons with headers, but before the full resonse is downloaded

    top read res call response.text() or response.json()

### Error Handling

use .catch to handle errors

when promise rejects, control jumps to the closest rejection handler down the chain

promise has invisible try..catch around it

## Promise API

### Promise.resolve

returns a resolved promise with the given value

used when we already have a value
    but would like to have it wrappd in a promise

### Promise.reject

creates a rejected promise with an error

### Promise.all

run many promises in parallel and wait till all of them finish

takes an iterable obj with promises
    usually an array

returns a new promise
    resolves when all of them are settle and has an array of their results

relative order is the same, no matter how long each take

common trick:
    map an array of job data into an array of promises and then wrap that into Promise.all

rejection error becomes out come of the whole Promise.all

no way to cancel or abort execution
    other promises continue to execute, but ultimately ignored

### Promise.race

takes an iterable of promises
    waits for the first res or error and goes on that


# Async/Await

## Async functions

`async` keyword placed before functions
    function always returns a promise

    wraps non promises into that promise

## Await

only works in `async` functions

`let value = await promise;`

makes JS wait until that promise settles and returns result

won't work in top-level code
    need to have a wrapping async function for the code that awaits

accepts thenables

class method can also be async

## Error Handling

if rejected, throws error

`try..catch` tends to be more convenient

`async/await` works well with `Promise.all`

# Currying and Partials

not only can we `bind` thids, but also args

partial function application
    creating a new function by fixing some params of the existing one

    no this? use `null`

    independent function with readable name

    have generic func and want a less universal variant for convenience

## Currying

translating a function from callable `f(a, b, c)` to 'f(a)(b)(c)'

can keep funtion callable normally and get partials easily