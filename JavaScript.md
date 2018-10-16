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


