## Features

- Convert any object into one that supports private, immutable properties.
- Leverages the Proxy object.
- Objects are inspectable, and non-private properties are mutable/inspectable.

## Getting Started

```
yarn install private-proxy

const pp = require('private-proxy');

const myObject = pp({});

myObject.dog = 'Fido';
console.log(myObject);
//=> {}

console.log(myObject.dog);
//=> 'Fido'
```

## Examples

#### Works with any objects, including classes

```
const pp = require('private-proxy');

class Person {
  constructor(name) {
    this.name = name; //Non-private property
  }
}

const me = pp(new Person('Rob')); //Any properties defined hereafter are private

```
#### Object keeps prototype
```
console.log(me);
//=> Person { name: 'Rob' }
```
#### Any property not defined before conversion can be set, but not inspected
```
me.age = 30; // me.age is a private property as it was not defined prior to conversion
console.log(me);
//=> Person { name: 'Rob' }
```
#### But can be accessed directly
```
console.log(me.age);
//=> 30
```
#### Non-private properties remain mutable
```
me.name = 'Joey';
console.log(me);
//=> Person { name: 'Joey' }
```
#### Private properties are immutable
```
me.age = 35;
console.log(me.age);
//=> 30
```
#### Undefined properties return undefined
```
console.log(me.dog);
//=> undefined
```