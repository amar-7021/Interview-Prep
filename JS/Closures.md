## Closures in JavaScript

### Theory

A **closure** is created when a function "remembers" the variables from its outer (lexical) scope even after that outer function has finished executing.

> **"Functions remember where they were created."**

### 🧠 Concept

A closure lets an inner function access variables from an outer function, even after the outer function has returned.

### ✅ Example

```js
function outerFunction() {
    const message = "Hello from the outer function!";

    return function innerFunction() {
        console.log(message); // ✅ Still has access!
    };
}

const greet = outerFunction();
greet(); // "Hello from the outer function!"
```

Even though `outerFunction` has finished running, the returned `innerFunction` still has access to `message`. That’s a closure!

---

### 🛠️ Practical Use Cases

#### 1. Data Privacy (like private variables)

```js
function createCounter() {
    let count = 0;

    return function () {
        count++;
        console.log(count);
    };
}

const counter = createCounter();
counter(); // 1
counter(); // 2
counter(); // 3
```

`count` is not accessible from the outside. It's "locked in" — only the returned function can interact with it.

#### 2. Function Factories

```js
function makeMultiplier(multiplier) {
    return function (num) {
        return num * multiplier;
    };
}

const double = makeMultiplier(2);
const triple = makeMultiplier(3);

console.log(double(5)); // 10
console.log(triple(5)); // 15
```

Closures allow the inner functions to "remember" the `multiplier` value passed to `makeMultiplier`.

---

### 🔄 Closures + Loops (Common Gotcha)

```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000);
}
// Output after 1 sec: 3, 3, 3 — not 0, 1, 2!
```

Why? Because `var` is function-scoped. The closure closes over the same `i`, which ends up as 3.

#### ✅ Fix with `let`:

```js
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000);
}
// Output: 0, 1, 2
```

---

### 🧠 Summary

A **closure** is a function + its **lexical environment**.

Closures let functions remember and access variables from the scope in which they were created.

#### They’re super useful for:

* Data encapsulation
* Currying and function factories
* Event handlers and callbacks
* Working with async code
