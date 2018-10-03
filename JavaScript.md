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

