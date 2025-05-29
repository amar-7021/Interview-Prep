## Arrow Functions in JavaScript

### Theory

Arrow functions in JavaScript are a shorter, cleaner way to write functions, introduced in ES6 (ECMAScript 2015). They're especially useful for writing concise callbacks and keeping code readable.

### Basic Syntax

```js
const add = (a, b) => a + b;
```

### ✅ Examples

#### 1. No Parameters

```js
const greet = () => console.log("Hello!");
```

#### 2. One Parameter (no need for parentheses)

```js
const square = x => x * x;
```

#### 3. Multiple Parameters

```js
const multiply = (a, b) => a * b;
```

#### 4. Block Body (with return)

Use curly braces `{}` if you need multiple lines or logic.

```js
const divide = (a, b) => {
  if (b === 0) return "Cannot divide by 0";
  return a / b;
};
```

### ❗️Important Differences vs. Regular Functions

#### 1. No `this` Binding

Arrow functions don’t have their own `this` — they inherit `this` from their surrounding scope (lexical `this`).

Example:

```js
function Timer() {
  this.seconds = 0;
  setInterval(() => {
    this.seconds++;
    console.log(this.seconds);
  }, 1000);
}
```

Using a regular function inside `setInterval` would not work the same, because `this` would refer to the global object or be `undefined`.

#### 2. No `arguments` Object

Arrow functions do not have their own `arguments` object.

```js
const showArgs = () => {
  console.log(arguments); // ❌ ReferenceError
};
```

If you need arguments, use a regular function or rest parameters:

```js
const showArgs = (...args) => {
  console.log(args); // ✅ works
};
```

#### 3. Cannot be Used as Constructors

You can't use arrow functions with `new`.

```js
const Person = (name) => {
  this.name = name;
};

const p = new Person("Alice"); // ❌ TypeError
```

### ⚡️ When to Use Arrow Functions

* Short callbacks (like `map`, `filter`, `forEach`)
* Keeping lexical `this` in closures
* Functional programming style

### ⚠️ When Not to Use Arrow Functions

* When you need `this` to refer to the calling object
* When using as constructors
* When needing the `arguments` object

### 🚫 Arrow Functions: What Not to Do

Don't use arrow functions for:

1. Object Methods
2. Prototypes
3. Event Handlers
4. Constructors
