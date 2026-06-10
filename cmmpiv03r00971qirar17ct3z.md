---
title: "Variables and Data Types in JavaScript"
seoTitle: "Variables and Data Types in JavaScript"
seoDescription: "Understand JavaScript variables and data types from scratch. Covers let, const, var, scope, and all 7 primitive types with clear code examples."
datePublished: 2026-03-13T23:22:35.465Z
cuid: cmmpiv03r00971qirar17ct3z
slug: variables-and-data-types-in-javascript
cover: https://cdn.hashnode.com/uploads/covers/6836cc7a1c8efb431960e9f0/fd663b4a-60c6-4b81-a9cb-1bf7332017d6.png
tags: variables, javascript, scope, datatypes, variable-declaration, variables-and-constants, scope-in-js, data-types-in-javascript, let-vs-var

---

Every program you write needs to store information. A user's name, a price, a list of items in a cart, all of that has to live somewhere. In JavaScript, variables are how you hold onto that information.

## **What is a Variable?**

Think of a variable as a labeled container. You put something inside it, and whenever you need that thing, you just call it by its label.

```javascript
let city = "Mumbai";
```

Here, `city` is the label and `"Mumbai"` is what is stored inside. Whenever you use `city` in your code, JavaScript fetches whatever is inside that container.

There is a second way to think about it:

A variable is a reference. It does not literally hold the value the way a box holds an apple. It points to a location in memory where the value lives. For numbers and strings this distinction barely matters day to day, but for objects and arrays it becomes very real. Two variables can point to the same thing in memory, which means changing one will affect the other.

```javascript
let a = { name: "Shravan" };
let b = a;

b.name = "Hitesh";
console.log(a.name); // "Hitesh"
```

Both `a` and `b` are references pointing at the same object. That is the reference model in action.

### **Declaring Variables in JavaScript**

JavaScript gives you three keywords to declare variables: `var`, `let`, and `const`.

```javascript
var age = 25;
let username = "shravan_dev";
const PI = 3.14159;
```

`var` is the original way to declare a variable. It has been in JavaScript since the beginning, but it comes with behavior that trips people up.

`let` is what you should reach for when you need a variable whose value will change over time.

`const` is for values you do not plan to reassign. Worth noting: `const` does not make something fully immutable. You can still add items to a `const` array or modify properties on a `const` object. It just means you cannot point that variable name at something entirely new.

```javascript
const colors = ["red", "blue"];
colors.push("green"); // this works
colors = ["yellow"];  // TypeError: Assignment to constant variable
```

* * *

### **Why Use** `let` **Instead of** `var`**?**

![](https://cdn.hashnode.com/uploads/covers/6836cc7a1c8efb431960e9f0/7f048910-0b7c-4a4d-ae18-5cc6f76bc139.png align="center")

The issue is scope. `var` is function-scoped, which means it leaks out of `if` blocks, `for` loops, and other structures wrapped in curly braces that are not functions. `let` and `const` are block-scoped, so they stay exactly where you put them.

```js
if (true) {
  var x = 10;
  let y = 20;
}

console.log(x); // 10 (leaked out)
console.log(y); // ReferenceError
```

### **What is Scope?**

![](https://cdn.hashnode.com/uploads/covers/6836cc7a1c8efb431960e9f0/bf6f9e37-db03-46a0-a8e5-c72a85ca92d1.png align="center")

Scope is the rule that decides where in your code a variable is accessible. Declare a variable inside a function, and code outside that function cannot see it. That boundary is scope.

```javascript
function greet() {
  let message = "Hello!";
  console.log(message); // works
}

console.log(message); // ReferenceError: message is not defined
```

JavaScript has three main levels of scope.

Global scope means the variable is declared outside any function or block and is accessible everywhere.

```javascript
let appName = "Servify"; // available everywhere
```

Function scope means the variable is declared inside a function and only accessible within it.

```javascript
function calculate() {
  let result = 42;
  return result;
}
// result is not accessible out here
```

Block scope means the variable is declared inside curly braces with `let` or `const` and only lives inside that block.

```javascript
if (true) {
  let blockVar = "I'm block scoped";
  console.log(blockVar); // works
}
console.log(blockVar); // ReferenceError
```

The innermost layer can read variables from outer layers, but outer layers cannot read inward. The block can see the function scope and the global scope. The function scope cannot see inside the block. The global scope sees nothing inside either.

## **What are Data Types?**

Every value in JavaScript has a type. That type tells the JavaScript engine what kind of data it is working with and what operations make sense on it. You cannot multiply a string the same way you multiply a number, and the type system is how JavaScript keeps track of that.

JavaScript divides its types into two categories: primitive and non-primitive.

### **The 7 Primitive Data Types**

Primitive values are simple and stored directly. When you copy a primitive, you get a real copy, not a reference.

**String**: text, wrapped in single quotes, double quotes, or backticks.

```javascript
let name = "Shravan";
let greeting = `Hello, ${name}!`;
```

**Number**: integers and decimals are both just `number` in JavaScript. There is no separate integer type.

```javascript
let age = 22;
let price = 99.99;
```

**Boolean**: either `true` or `false`. Used heavily in conditions and comparisons.

```javascript
let isLoggedIn = true;
let hasPaid = false;
```

**Undefined**: a variable that has been declared but not yet given a value.

```javascript
let score;
console.log(score); // undefined
```

**Null**: an intentional absence of value. You set this on purpose when you want to say "there is nothing here right now."

```javascript
let selectedUser = null;
```

**Symbol**: a guaranteed unique value. Used mostly when building libraries or needing keys that will never accidentally collide.

```javascript
let id = Symbol("userId");
```

**BigInt**: for integers too large for the regular `Number` type to handle accurately.

```javascript
let hugeNumber = 9007199254740991n;
```

### **Non-Primitive Data Types**

Non-primitive types are stored by reference, not by value. They can hold collections of data and grow in complexity.

**Object**: a collection of key-value pairs. The most fundamental non-primitive in JavaScript.

```js
let user = {
  name: "Shravan",
  age: 22,
  isStudent: true
};

console.log(user.name); // "Shravan"
```

Objects can hold any type of value, including other objects and arrays.

**Array**: a special kind of object built for ordered lists. Arrays use zero-based indexing, so the first item sits at position 0.

```js
let fruits = ["mango", "banana", "apple"];

console.log(fruits[0]); // "mango"
console.log(fruits.length); // 3
```

Arrays come with built-in methods like `.push()`, `.pop()`, `.map()`, and `.filter()` that make working with lists much more convenient.

The difference between primitives and non-primitives comes back to what we covered at the start. Copy a primitive and you get a new independent value. Copy an object or array and both variables point to the same thing in memory.

## **Wrapping Up**

Variables and data types are where every JavaScript program begins. You declare a variable to hold a value, pick the right keyword based on whether that value will change, and understand the type of data you are working with so you can operate on it correctly.

`let` and `const` are the standard today. `var` is worth knowing about but not worth reaching for. Primitives give you simple standalone values. Objects and arrays let you build more complex structures. Scope keeps your variables from stepping on each other.

Once these feel natural, everything else in JavaScript gets easier to understand.