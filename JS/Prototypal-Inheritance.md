# Inheritance using Classes (Prototypal Inheritance)

## Theory

### Constructor Functions
🔹 ** What is a Constructor Function ?**
    A constructor function is a regular function used with the`new` keyword to create new objects.

```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;

    this.greet = function () {
        return `Hi, I'm ${this.name} and I'm ${ this.age } years old.`;
    };
}

const p1 = new Person("Alice", 30);
console.log(p1.greet()); // Hi, I'm Alice and I'm 30 years old.
```

### ⚠️ Optimization Tip: Use the Prototype for Shared Methods
🔹 ** Instead of adding methods inside the constructor (which creates a new copy for every instance), put shared methods on the prototype:

```js
function Person(name, age) {
    this.name = name;
    this.age = age;
}

Person.prototype.greet = function () {
    return `Hi, I'm ${this.name} and I'm ${this.age} years old.`;
}; // This saves memory because all instances share the same greet function.
```

### Classes (ES6+)
🔷 What is a Class?
A class is a newer, cleaner way to define constructor functions and prototypes. It's syntactic sugar — under the hood, it still uses prototypes.

```js
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    greet() {
        return `Hi, I'm ${this.name} and I'm ${this.age} years old.`;
    }
}

const p2 = new Person("Bob", 25);
console.log(p2.greet()); // Hi, I'm Bob and I'm 25 years old.
```

## Key Points:

* The constructor() method is where you set up the object (just like a constructor function).

* Other methods (like greet()) are automatically put on the prototype.

* Classes must be used with new. Calling them without new will throw an error.

## Factory Function vs Constructor Function vs Class — Side-by-Side
| Feature                | Factory Function        | Constructor Function      | Class               |
|-----------------------|-------------------------|--------------------------|---------------------|
| **Syntax Style**       | Functional pattern      | Older (ES5)              | Cleaner, modern (ES6+) |
| **Uses `this`**        | ❌ No                   | ✅ Yes                   | ✅ Yes              |
| **Needs `new`**        | ❌ No                   | ✅ Yes                   | ✅ Yes (throws error without it) |
| **Method Sharing**     | ❌ Per-instance copies  | ✅ Manually set on prototype | ✅ Automatically handled |
| **Private Fields**     | ✅ Yes (via closure)     | ❌ No (needs closure)     | ✅ Yes (`#private` syntax) |
| **Inheritance**        | ❌ Manual composition   | ✅ Manual via `Object.create` & `.call()` | ✅ Simple with `extends` & `super` |
---

### Key Points:
* The constructor() method is where you set up the object (just like a constructor function).

* Other methods (like greet()) are automatically put on the prototype.

* Classes must be used with new. Calling them without new will throw an error.

### Constructor Function vs Class — Side-by-Side

| Feature                | Constructor Function      | Class                    |
|-----------------------|--------------------------|--------------------------|
| **Syntax Style**       | Older (ES5)              | Cleaner, modern (ES6+)   |
| **Uses `this`**        | ✅ Yes                   | ✅ Yes                   |
| **Needs `new`**        | ✅ Yes                   | ✅ Yes (throws error without it) |
| **Method Sharing**     | Manually set on prototype | Automatically handled    |
| **Private Fields**     | ❌ (needs closure)        | ✅ via `#private` syntax  |
| **Inheritance**        | Manual via `Object.create` & `.call()` | Simple with `extends` & `super` |


### Summary 

* Use constructor functions if you’re working in older environments or want low-level control.

* Use classes for modern code — they’re easier to read and maintain.

* Both can be used to create objects and share methods through prototypes.

```js
class Person {
    talk() {
        return 'Talking';
    }
}
const me = new Person();
const you = new Person();
me.talk(); // Talking
you.talk(); // Talking

// To update the function for both instances you only have to do it once:
Person.prototype.talk = function () {
    return 'New and improved Talking';
};

```


### Inheritance using a Constructor Function
```js
function Person() { };
Person.prototype.talk = function () {
    return 'Talking';
}

const me = new Person();
const you = new Person();
me.talk(); // Talking
you.talk(); // Talking
```

### Inheritance using pure objects with Object.create

```js
const person = {
    talk() {
        return 'Talking';
    }
}
const me = Object.create(person);
me.talk(); // Talking
```


### Inheritance using pure objects with Object.setPrototypeOf
```js
const person = {}
person.__proto__.talk = function () {
    return 'Talking';
}
const me = {};
Object.setPrototypeOf(me, person);
me.talk(); // Talking
```

### Extending a Class using 'extends'
```js
class Person {
    talk() {
        return 'talking';
    }
}

class SuperHuman extends Person {
    fly() {
        return 'flying';
    }
}
const me = new Person();
console.log(me.talk); // talk exists
console.log(me.fly); // fly does NOT exists

const you = new SuperHuman();
console.log(you.fly); // fly exists
console.log(you.talk); // talk also exists!
```

### Why use Inheritance
 1. If you have objects that have shared behavior
 2. If you have components that have shared functionality


