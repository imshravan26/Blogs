---
title: "JavaScript Operators and Expressions"
seoTitle: "JavaScript Operators and Expressions"
seoDescription: "Master the Core Tools That Power Every Line of JavaScript"
datePublished: 2026-03-07T13:11:57.093Z
cuid: cmmgcelr600dn2eq97q3k97ew
slug: javascript-operators-and-expressions
cover: https://cdn.hashnode.com/uploads/covers/6836cc7a1c8efb431960e9f0/2107def8-6c58-4fd5-9e2f-f914be5ffda6.png
tags: javascript, basics, operators, basics-of-javascript

---

## What Are Operators?

An **operator** is a special symbol or keyword in JavaScript that performs a specific operation on one or more values. The values that operators act upon are called **operands**.

For example:

```js
5 + 3
```

Here, `+` is the **operator** and `5` and `3` are the **operands**. Together, they form an **expression** that evaluates to `8`.

### What Are Expressions?

An **expression** is any valid unit of code that **resolves to a value**. In simple terms, whenever you write a piece of code that produces a result, you are writing an expression.

For example:

```js
10 + 5       // evaluates to 15
x = 20       // evaluates to 20
5 > 3        // evaluates to true
```

Every one of the above lines is an expression because each one produces a value.

## Types of Operators in JavaScript

### 1\. Arithmetic Operators

Arithmetic operators are used to perform **mathematical calculations** between numeric values.

| Operator | Name | Example | Result |
| --- | --- | --- | --- |
| `+` | Addition | `10 + 5` | `15` |
| `-` | Subtraction | `10 - 5` | `5` |
| `*` | Multiplication | `10 * 5` | `50` |
| `/` | Division | `10 / 5` | `2` |
| `%` | Modulus | `10 % 3` | `1` |
| `**` | Exponentiation | `2 ** 4` | `16` |
| `++` | Increment | `x++` | adds 1 |
| `--` | Decrement | `x--` | subtracts 1 |

**Example:**

```javascript
let a = 10;
let b = 3;

console.log(a + b);   // 13
console.log(a - b);   // 7
console.log(a * b);   // 30
console.log(a / b);   // 3.33
console.log(a % b);   // 1
console.log(a ** b);  // 1000
```

### 2\. Comparison Operators

Comparison operators are used to **compare two values** and always return either `true` or `false`.

| Operator | Name | Example | Result |
| --- | --- | --- | --- |
| `==` | Equal to | `5 == "5"` | `true` |
| `===` | Strict equal to | `5 === "5"` | `false` |
| `!=` | Not equal to | `5 != 3` | `true` |
| `!==` | Strict not equal to | `5 !== "5"` | `true` |
| `>` | Greater than | `10 > 5` | `true` |
| `<` | Less than | `10 < 5` | `false` |
| `>=` | Greater than or equal | `5 >= 5` | `true` |
| `<=` | Less than or equal | `3 <= 5` | `true` |

**Example:**

```js
let x = 10;
let y = 20;

console.log(x == y);    // false
console.log(x != y);    // true
console.log(x > y);     // false
console.log(x < y);     // true
console.log(x === 10);  // true
console.log(x !== "10"); // true  ← strict check
```

> 💡 **Tip:** Always prefer `===` over `==` in JavaScript. The `==` operator does type conversion which can lead to unexpected results, while `===` checks both value and type.

### 3\. Logical Operators

Logical operators are used to **combine or reverse boolean expressions** and are heavily used in conditions and decision making.

| Operator | Name | Description | Example | Result |
| --- | --- | --- | --- | --- |
| `&&` | AND | Returns `true` if **both** conditions are true | `true && false` | `false` |
| `||` | OR | Returns `true` if **at least one** condition is true | `true || false` | `true` |
| `!` | NOT | **Reverses** the boolean value | `!true` | `false` |

**Example:**

js

```javascript
let age = 20;
let hasID = true;

// AND - both must be true
console.log(age >= 18 && hasID);   // true

// OR - at least one must be true
console.log(age < 18 || hasID);    // true

// NOT - reverses the value
console.log(!hasID);               // false
```

> 💡 **Tip:** Logical operators don't always return `true` or `false` — they return the **actual value** of one of the operands. This is called **short-circuit evaluation**.

```javascript
console.log(0 || "hello");   // "hello"  ← returns first truthy value
console.log(1 && "hello");   // "hello"  ← returns last truthy value
```

### 4\. Assignment Operators

Assignment operators are used to **assign or update values** stored in variables.

| Operator | Name | Example | Equivalent to |
| --- | --- | --- | --- |
| `=` | Assignment | `x = 10` | `x = 10` |
| `+=` | Add and assign | `x += 5` | `x = x + 5` |
| `-=` | Subtract and assign | `x -= 5` | `x = x - 5` |
| `*=` | Multiply and assign | `x *= 5` | `x = x * 5` |
| `/=` | Divide and assign | `x /= 5` | `x = x / 5` |
| `%=` | Modulus and assign | `x %= 3` | `x = x % 3` |
| `**=` | Exponent and assign | `x **= 2` | `x = x ** 2` |

**Example:**

```js
let x = 10;

x += 5;   console.log(x);  // 15
x -= 3;   console.log(x);  // 12
x *= 2;   console.log(x);  // 24
x /= 4;   console.log(x);  // 6
x %= 4;   console.log(x);  // 2
x **= 3;  console.log(x);  // 8
```

## Conclusion

Operators and expressions are the building blocks of any JavaScript program. Operators (like `+`, `===`, `&&`) perform operations on operands, and expressions are pieces of code that evaluate to values. Understanding the different operator types—arithmetic, comparison, logical, assignment, and others—lets you write clearer, more predictable code.

Keep these practical tips in mind:

*   Prefer strict equality (`===` / `!==`) to avoid unexpected type coercion.
    
*   Learn operator precedence and use parentheses to make intent explicit.
    
*   Remember short-circuit behavior for logical operators (`&&`, `||`) when controlling evaluation flow.
    
*   Watch out for edge cases (e.g., `NaN`, `null`, `undefined`) and implicit conversions.
    

Mastering operators and expressions will make debugging easier and help you write more robust JavaScript. For deeper reference and examples, consult documentation such as MDN Web Docs.