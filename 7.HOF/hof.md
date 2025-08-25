**Higher-Order Functions (HOFs)** in **JavaScript** in **depth**—definition, characteristics, real-world use, examples, interview concepts, and tricky points.

---

## **What is a Higher-Order Function (HOF)?**

A **Higher-Order Function** is a function that does **at least one** of the following:

1. **Takes another function as an argument (callback).**
2. **Returns a new function.**

In short: **Functions that operate on other functions.**

---

### **Why do we have HOFs in JavaScript?**

Because **functions are first-class citizens** in JS:
(Meaning: that functions are treated like any other value or object in the language)

- Functions can be stored in variables.
- Functions can be passed as arguments.
- Functions can be returned from other functions.

---

## **Basic Example**

```js
function greet(name) {
  return `Hello, ${name}`;
}

function processUserInput(callback) {
  const name = "Alice";
  console.log(callback(name));
}

processUserInput(greet);
Output: Hello, Alice;
```

Here:

- `processUserInput` is a **HOF** because it **takes a function (`greet`) as an argument**.

---

## **Characteristics of HOF**

- Uses **callback functions**.
- Often used for **abstraction** and **reusability**.
- Common in **functional programming**.

---

## **Why are HOFs important?**

- Make code **clean and modular**.
- Used in **map, filter, reduce**, **event handling**, **promises**, **async/await**.
- Core of **functional programming style**.

---

## **Common Built-in Higher-Order Functions in JS**

### 1. **`map()`**

- Creates a new array by applying a function to each element.

```js
const nums = [1, 2, 3];
const squared = nums.map((n) => n * n);
console.log(squared);
[1, 4, 9];
```

### 2. **`filter()`**

- Creates a new array with elements that pass a condition.

```js
const nums = [1, 2, 3, 4];
const evens = nums.filter((n) => n % 2 === 0);
console.log(evens);
[2, 4];
```

### 3. **`reduce()`**

- Reduces an array to a single value.

```js
const nums = [1, 2, 3];
const sum = nums.reduce((acc, curr) => acc + curr, 0);
console.log(sum);
6;
```

### 4. **`forEach()`**

- Iterates over elements but doesn’t return a new array.

```js
[1, 2, 3].forEach((n) => console.log(n));
```

### 5. **`sort()`**

- Takes a comparator function.

```js
[3, 1, 2].sort((a, b) => a - b);
```

---

## **HOF Returning Functions**

```js
function multiplier(factor) {
  return function (number) {
    return number * factor;
  };
}

const double = multiplier(2);
console.log(double(5));
10;
```

Here, `multiplier` is a **HOF** because it **returns a function**.

---

## **Real-World Use Cases**

1. **Event Listeners**

```js
document.getElementById("btn").addEventListener("click", () => {
  console.log("Button clicked!");
});
```

2. **Timers**

```js
setTimeout(() => console.log("Hello after 2s"), 2000);
```

3. **Middleware in Express.js**

```js
app.use((req, res, next) => {
  console.log("Middleware executed");
  next();
});
```

---

## **HOF vs Callback**

- **Callback:** The function you pass **into** another function.
- **HOF:** The function that **accepts or returns another function**.

---

## **Benefits**

- **Reusability**: DRY code.
- **Abstraction**: Hide details.
- **Functional style**: Encourages immutability and side-effect-free code.

---

## **Important Interview Questions**

1. What is a higher-order function?
2. Difference between **HOF** and **callback**?
3. Implement your own `map()` using HOF.
4. Explain how `reduce()` works internally.
5. Why do we use HOF in async programming?

---

### **Tricky Interview Questions**

#### Q1:

What will be logged?

```js
function outer() {
  return function inner() {
    return "Hello";
  };
}
console.log(outer()());
```

Output: `"Hello"`

---

#### Q2:

Create a function `once(fn)` that runs the function only once.

```js
function once(fn) {
  let called = false;
  return function () {
    if (!called) {
      called = true;
      return fn();
    }
  };
}

const sayHi = once(() => console.log("Hi"));
sayHi();
Hi;
sayHi();
nothing;
```

---

### **Mini Coding Challenge**

1. Implement `myMap()` using `forEach()`.
2. Write a function `compose()` that takes two functions and returns a new function (composition).
3. Create a `multiplier(factor)` function (returns a new function).
4. Implement a custom `filter()` without using the built-in one.
5. Write a HOF that takes a function and delays its execution by 2 seconds.

---

**Example of Higher-Order Functions in JavaScript** combination of **`map()`, `filter()`, and `reduce()`** for data transformation.

---

### **Example: Calculate the total price of products over $500 after applying a 10% discount**

```js
const products = [
  { name: "Laptop", price: 1000 },
  { name: "Phone", price: 400 },
  { name: "Tablet", price: 600 }
];

const total = products
  .filter(product => product.price > 500)           Keep products > $500
  .map(product => product.price * 0.9)              Apply 10% discount
  .reduce((acc, price) => acc + price, 0);          Sum prices

console.log(total); Output: 1440 (900 for Laptop + 540 for Tablet)
```

---

### **Why this?**

- It shows **functional programming style** in JS.
- It uses **three built-in HOFs**:
  - `filter()` → takes a function as argument.
  - `map()` → takes a function as argument.
  - `reduce()` → takes a function as argument.
- It makes code **clean and expressive** (no `for` loops).

---

### **Step-by-step:**

1. **Filter** → Removes `Phone` because price ≤ 500.
   → `[ { name: "Laptop", price: 1000 }, { name: "Tablet", price: 600 } ]`
2. **Map** → Applies 10% discount:
   → `[900, 540]`
3. **Reduce** → Adds values:
   → `1440`
