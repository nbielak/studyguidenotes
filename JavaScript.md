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
