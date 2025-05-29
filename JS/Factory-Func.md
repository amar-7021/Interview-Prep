## Factory Functions in JavaScript

### Theory

A **factory function** is a regular function that creates and returns an object.

> It’s called a "factory" because it produces objects, just like a real-world factory produces products.

### 🔧 Basic Example

```js
function createPerson(name, age) {
    return {
        name,
        age,
        greet() {
            return `Hi, I'm ${this.name} and I'm ${this.age} years old.`;
        }
    };
}

const person1 = createPerson("Alice", 30);
console.log(person1.greet()); // Hi, I'm Alice and I'm 30 years old.
```

---

### ✅ Why Use Factory Functions?

| Benefit              | Description                                                               |
| -------------------- | ------------------------------------------------------------------------- |
| ✔️ No `new` keyword  | Unlike constructors or classes, you don’t need `new` to create an object. |
| ✔️ Cleaner syntax    | No weird `this` behavior unless you want it.                              |
| ✔️ Private variables | Use closures to hide data.                                                |
| ✔️ Flexible          | Can return anything (objects, functions, other factories).                |
| ✔️ Easy to compose   | Combine multiple factory functions together. Great for modular code.      |

---

### 🔒 Factory Functions + Encapsulation (Closures)

```js
function createCounter() {
    let count = 0; // private

    return {
        increment() {
            count++;
            return count;
        },
        decrement() {
            count--;
            return count;
        },
        getCount() {
            return count;
        }
    };
}

const counter = createCounter();
console.log(counter.increment()); // 1
console.log(counter.increment()); // 2
console.log(counter.getCount());  // 2
```

`count` is private. Only the returned methods can access and modify it.

---

### ⚠️ Factory Function vs Constructor vs Class

| Feature            | Factory Function        | Constructor Function      | Class               |
| ------------------ | ----------------------- | ------------------------- | ------------------- |
| Requires `new`?    | ❌ No                    | ✅ Yes                     | ✅ Yes               |
| Private variables? | ✅ Yes (via closure)     | ❌ No (unless using hacks) | ✅ Yes (`#` syntax)  |
| Syntax simplicity  | ✅ Very simple           | 😐 Older style            | ✅ Modern & readable |
| Shared methods?    | ❌ Not shared by default | ✅ via prototype           | ✅ via prototype     |

---

### 🧪 Bonus: Factory with Shared Behavior (Composition)

You can compose behaviors instead of using inheritance.

```js
const talker = (name) => ({
    talk: () => `${name} is talking`
});

const walker = (name) => ({
    walk: () => `${name} is walking`
});

function createPerson(name) {
    return {
        name,
        ...talker(name),
        ...walker(name)
    };
}

const joe = createPerson("Joe");
console.log(joe.talk()); // Joe is talking
console.log(joe.walk()); // Joe is walking
```

This modular design avoids class hierarchies and promotes code reuse.

---

### 🧠 Summary

* A **factory function** is a function that returns a new object.
* It's an alternative to `class` or `constructor` for object creation.
* Allows **encapsulation**, **simplicity**, and **modular design**.
* Great for when you don't need inheritance or want functional-style flexibility.
