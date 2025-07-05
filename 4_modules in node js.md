# 📦 Node.js Modules, Exports, Imports & JSON – Complete Guide

---

## 📘 What is a Module?

A **module** is a **self-contained piece of code** that encapsulates its logic.

- Every `.js` file in Node.js is treated as a **separate module**.
- Code inside a module is **private by default**.
- Modules promote **clean, modular, and reusable** code.

```js
// myModule.js
let x = 10;
console.log("I am a module");
```

---

## ✅ How to Add Code from Another Module

To bring code from one module into another, use the `require()` function.

```js
// app.js
require("./two.js"); // One module into another

let a = 10;
let b = 20;
console.log("Sum is:", a + b);

// Output:
// Code in two.js runs first
// Then rest of app.js is executed
```

📌 Node.js **executes the imported module first**, then continues with the current code.

---

## ❌ Why You Can’t Use Imported Variables Directly

Just using `require()` does **not expose** variables or functions to the current file.

```js
// two.js
let age = 25;

// app.js
require("./two.js");
console.log(age); // ❌ ReferenceError
```

### 🛡️ Why?

- Each module has its **own scope**.
- This **prevents conflicts** when multiple modules have variables with the same name.
- This is the **default behavior in Node.js**.

---

## ✅ Exporting and Importing Data Between Modules

### ✨ Exporting a Single Value

```js
// two.js
let age = 25;
module.exports = age; // Note: 'module.exports', not 'export'

// app.js
const newAge = require("./two.js");
console.log(newAge); // 25
```

---

### 🔁 Exporting Multiple Values Using an Object

Wrap everything you want to export in an object.

```js
// two.js
let age = 30;
let name = "John";
module.exports = { age, name };

// app.js
const { age, name } = require("./two.js"); // Destructure on the fly
console.log(age);  // 30
console.log(name); // John

// OR:
const variables = require("./two.js");
console.log(variables.age);
console.log(variables.name);
```

---

### 🧪 Another Way to Export (Adding Properties)

Since `module.exports` is an empty object by default, you can add properties like this:

```js
// two.js
let age = 40;
let name = "Alice";

module.exports.age = age;
module.exports.name = name;
```

---

## 📂 Importing `.json` Files in Node.js

Node.js supports importing `.json` files directly.

```js
// data.json
{
  "age": 22,
  "name": "Leo"
}

// app.js
const data = require("./data.json");
console.log(data.name); // Leo
```

✅ JSON is automatically parsed into a JavaScript object.

---

## 🔐 Why Modules Are Private by Default

- Avoids **name conflicts** across files.
- Helps maintain **encapsulation** and **modularity**.
- You **must explicitly export** anything you want to share.

---

## 💡 Best Practice

✅ While exporting: **wrap everything in an object**

✅ While importing: **destructure on the fly**

```js
// Export
module.exports = { age, name };

// Import
const { age, name } = require("./two.js");
```

---

## 📊 CommonJS vs ES Modules (ESM)

| Feature                              | CommonJS (`.cjs`)         | ES Modules (`.mjs`)               |
|--------------------------------------|---------------------------|-----------------------------------|
| Export syntax                        | `module.exports`          | `export`                          |
| Import syntax                        | `require()`               | `import`                          |
| Default in                           | Node.js                   | React, Angular (modern tools)     |
| Age                                  | Older                     | Newer (ES6+)                      |
| Execution style                      | Synchronous               | Asynchronous available            |
| Scope mode                           | Non-strict                | Strict (by default)               |
| Hoisting                             | Allowed                   | Not allowed                       |
| Can run this? `z = 100`              | ✅ Yes (loose mode)       | ❌ No (`ReferenceError`)          |

---

### ⚙️ Switching Between Module Types

To switch between CommonJS and ESM, update your `package.json`:

#### ➤ For ES Modules (ESM):
```json
{
  "type": "module"
}
```

#### ➤ For CommonJS (default):
```json
{
  "type": "commonjs"
}
```

---

## 🧱 Grouping Multiple Files via a Middle Module

Say we have this folder:

```
project/
├── add.js
├── subtract.js
├── multiply.js
└── calculate.js   ← This will import and group the rest
```

### Step 1: Export Functions in Each File

```js
// add.js
module.exports = (a, b) => a + b;

// subtract.js
module.exports = (a, b) => a - b;

// multiply.js
module.exports = (a, b) => a * b;
```

### Step 2: Group in `calculate.js`

```js
const add = require("./add");
const subtract = require("./subtract");
const multiply = require("./multiply");

module.exports = { add, subtract, multiply };
```

### Step 3: Use in `app.js`

```js
const { add, subtract, multiply } = require("./calculate");

console.log(add(2, 3));       // 5
console.log(subtract(5, 2));  // 3
console.log(multiply(3, 4));  // 12
```

✅ This is called **file grouping**, and it's very useful for **project structure and reusability**.

---

## 📌 Summary Notes

- To import: use `require()`
- To export:
  - Use `module.exports = value`
  - Or `module.exports = { ... }` for multiple exports
- Module scope is private by default
- Destructure on import for cleaner code
- Use ESM (`import/export`) by setting `"type": "module"` in `package.json`

---
