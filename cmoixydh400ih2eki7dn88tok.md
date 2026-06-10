---
title: "Array Methods Every Developer Must Know"
seoTitle: "JavaScript Array Methods with Real Examples"
seoDescription: "Master JavaScript array methods with clear examples of map(), filter(), reduce(), push(), and pop."
datePublished: 2026-04-28T18:10:08.443Z
cuid: cmoixydh400ih2eki7dn88tok
slug: array-methods-every-developer-must-know
cover: https://cdn.hashnode.com/uploads/covers/6836cc7a1c8efb431960e9f0/37356b3a-e5ba-4692-baa1-af15391e0918.png
tags: foreach, map, array, reduce, filter, array-methods, array-javascript-array-methods-map-filter-foreach, array-in-javascript, map-in-js, filter-in-js, arrayfrom, arrayof

---

This article covers the full picture: how to create arrays with static methods, how to mutate them, how to read from them without changing them, and how to iterate over them with the powerful trio of `map`, `filter`, and `reduce`.

### Static Methods — Creating and Checking Arrays

These live on `Array` itself, not on an instance. You call them as `Array.something()`.

#### `Array.from()`

Converts anything iterable into a real array  
a string, a Set, a NodeList, a Map, even an object with a length.

```javascript
const citySet = new Set(["Mumbai", "Delhi", "Bangalore", "Mumbai", "Pune"]);

const cities = Array.from(citySet);

console.log(cities);
// Output: ["Mumbai", "Delhi", "Bangalore", "Pune"]
```

`Array.from` also accepts a mapping function as a second argument:

```javascript
const doubled = Array.from([1, 2, 3, 4], (n) => n*n );

console.log(doubled);
// Output: [2, 4, 6, 8]
```

#### `Array.of()`

Creates a new array from the arguments you pass. The reason this exists is a quirk in the old `Array()` constructor `Array(3)` creates three empty slots, not an array containing the number 3. `Array.of(3)` always does the intuitive thing.

```javascript
const scores = Array.of(85, 92, 78, 96);

console.log(scores);
// Output: [85, 92, 78, 96]
```

#### `Array.isArray()`

Checks whether something is genuinely an array. `typeof` won't help here, it returns `"object"` for arrays, objects, and `null` alike.

```javascript
function displayProducts(data) {
  if (Array.isArray(data)) {
    console.log("Multiple products:", data.length);
  } else {
    console.log("Single product:", data.name);
  }
}

displayProducts([{ name: "Shoes" }, { name: "Bag" }]);
// Output: "Multiple products: 2"

displayProducts({ name: "Watch" });
// Output: "Single product: Watch"
```

### Mutating Methods: Changing the Array in Place

These methods modify the original array directly.

#### `push()` and `pop()`

`push` adds one or more items to the end. `pop` removes the last item and returns it.

```javascript
const queue = ["Blinding Lights", "Levitating", "Stay"];

queue.push("Peaches");
console.log(queue);
// Output: ["Blinding Lights", "Levitating", "Stay", "Peaches"]

const removed = queue.pop();
console.log(removed);   // Output: "Peaches"
console.log(queue);     // Output: ["Blinding Lights", "Levitating", "Stay"]
```

#### `shift()` and `unshift()`

`shift` removes from the front and returns it. `unshift` adds to the front.

```javascript
const tickets = ["Ticket #102", "Ticket #103"];

tickets.unshift("Ticket #101 (URGENT)");
console.log(tickets);
// Output: ["Ticket #101 (URGENT)", "Ticket #102", "Ticket #103"]

const next = tickets.shift();
console.log(next);      // Output: "Ticket #101 (URGENT)"
console.log(tickets);   // Output: ["Ticket #102", "Ticket #103"]
```

#### `splice()`

The Swiss Army knife of array mutation. It can insert, remove, or replace elements at any position.

Syntax: `array.splice(startIndex, deleteCount, ...itemsToInsert)`

```javascript
const todos = ["Buy groceries", "Do laundry", "Clean kitchen"];

// Insert "Reply to emails" at index 1, delete 0 items
todos.splice(1, 0, "Reply to emails");
console.log(todos);
// Output: ["Buy groceries", "Reply to emails", "Do laundry", "Clean kitchen"]

// Remove "Do laundry" (now at index 2)
todos.splice(2, 1);
console.log(todos);
// Output: ["Buy groceries", "Reply to emails", "Clean kitchen"]
```

#### `sort()`

Sorts the array in place. Without a comparator, it converts elements to strings first, which causes infamous bugs with numbers.

```javascript
const prices = [199, 49, 1299, 89, 599];

// Wrong — lexicographic sort
prices.sort();
console.log(prices);
// Output: [1299, 199, 49, 589, 89] — incorrect!

// Correct — provide a comparator
prices.sort((a, b) => a - b);
console.log(prices);
// Output: [49, 89, 199, 599, 1299]
```

For strings, `sort()` without a comparator works fine:

```javascript
const names = ["Priya", "Aarav", "Zara", "Dev"];
names.sort();
console.log(names);
// Output: ["Aarav", "Dev", "Priya", "Zara"]
```

#### `reverse()`

Reverses the array in place.

```javascript
const steps = ["Write code", "Test", "Deploy", "Monitor"];

steps.reverse();
console.log(steps);
// Output: ["Monitor", "Deploy", "Test", "Write code"]
```

#### `fill()`

Fills some or all elements of an array with a static value.

```javascript
const board = new Array(9).fill(null);

console.log(board);
// Output: [null, null, null, null, null, null, null, null, null]

// Mark position 4 as "X"
board[4] = "X";
console.log(board);
// Output: [null, null, null, null, "X", null, null, null, null]
```

### Accessor Methods: Reading Without Changing

These return information or a new array. The original stays untouched.

#### `concat()`

Merges two or more arrays into a new one.

```javascript
const sectionA = ["Amit", "Bhavna", "Chirag"];
const sectionB = ["Deepa", "Eshan", "Fatima"];

const allStudents = sectionA.concat(sectionB);

console.log(allStudents);
// Output: ["Amit", "Bhavna", "Chirag", "Deepa", "Eshan", "Fatima"]

console.log(sectionA); // Original unchanged: ["Amit", "Bhavna", "Chirag"]
```

#### `includes()`

Returns `true` or `false` based on whether an element exists.

```javascript
const admins = ["shravan", "hitesh", "krish"];

console.log(admins.includes("shravan")); // Output: true
console.log(admins.includes("kaustubh")); // Output: false
```

#### `indexOf()` and `lastIndexOf()`

`indexOf` returns the first index where an element appears. `lastIndexOf` returns the last. Both return `-1` if not found.

```javascript
const visitLog = ["home", "pricing", "home", "docs", "home", "checkout"];

console.log(visitLog.indexOf("home"));     // Output: 0
console.log(visitLog.lastIndexOf("home")); // Output: 4
console.log(visitLog.indexOf("signup"));   // Output: -1
```

#### `join()`

Converts all array elements into a single string, using a separator you define.

```javascript
const breadcrumb = ["Home", "Electronics", "Laptops", "Gaming Laptops"];

const trail = breadcrumb.join(" > ");

console.log(trail);
// Output: "Home > Electronics > Laptops > Gaming Laptops"
```

### Iteration Methods: Doing Something With Each Element

This is where arrays get truly powerful.

#### `forEach()`

Runs a function once for every element. It doesn't return a new array — it's purely for side effects like logging, updating the DOM, or sending data.

```javascript
const orders = [
  { id: "ORD001", item: "Laptop", status: "Shipped" },
  { id: "ORD002", item: "Mouse", status: "Processing" },
  { id: "ORD003", item: "Keyboard", status: "Delivered" },
];

orders.forEach((order) => {
  console.log(`${order.id} — ${order.item} [${order.status}]`);
});

// Output:
// ORD001 — Laptop [Shipped]
// ORD002 — Mouse [Processing]
// ORD003 — Keyboard [Delivered]
```

**vs. for loop:**

```javascript
// Traditional for loop
for (let i = 0; i < orders.length; i++) {
  console.log(orders[i].id);
}

// forEach — same result, less noise
orders.forEach((order) => console.log(order.id));
```

`forEach` wins on readability when you don't need the index variable.

#### `map()`

![](https://cdn.hashnode.com/uploads/covers/6836cc7a1c8efb431960e9f0/489a0d7c-04e7-40ca-8a1f-234a1651b6c7.png align="center")

Creates a brand new array by transforming every element. The original is untouched.

```javascript
const pricesUSD = [10, 25, 50, 100];

const pricesINR = pricesUSD.map((price) => price * 83.5);

console.log(pricesINR);
// Output: [835, 2087.5, 4175, 8350]

console.log(pricesUSD); // Original unchanged: [10, 25, 50, 100]
```

Another example — extracting just one field from an array of objects:

```javascript
const users = [
  { name: "Shravan", age: 20 },
  { name: "Hitesh", age: 22 },
  { name: "Krish", age: 21 },
];

const names = users.map((user) => user.name);

console.log(names);
// Output: ["Shravan", "Hitesh", "Krish"]
```

#### `filter()`

![](https://cdn.hashnode.com/uploads/covers/6836cc7a1c8efb431960e9f0/675b8856-3275-4862-bff9-8386a061c39d.png align="center")

Creates a new array containing only the elements that pass a condition. Elements that fail the test are excluded.

```javascript
const candidates = [
  { name: "Ananya", experience: 1 },
  { name: "Rohan", experience: 4 },
  { name: "Simran", experience: 2 },
  { name: "Vikram", experience: 6 },
  { name: "Pooja", experience: 3 },
];

const qualified = candidates.filter((c) => c.experience >= 3);

console.log(qualified);
// Output:
// [
//   { name: "Rohan", experience: 4 },
//   { name: "Vikram", experience: 6 },
//   { name: "Pooja", experience: 3 }
// ]
```

#### `reduce()`

![](https://cdn.hashnode.com/uploads/covers/6836cc7a1c8efb431960e9f0/07424041-6369-457e-834f-12f5823c7d2c.png align="center")

Reduces an entire array down to a single value, a number, a string, an object, anything. It takes an accumulator (the running result) and the current element, and you define what happens at each step.

Think of it like tallying a bill. You start at 0, and for each item, you add its price to your running total.

```javascript
const sales = [1200, 450, 3000, 875, 2100];

const totalRevenue = sales.reduce((total, sale) => total + sale, 0);

console.log(totalRevenue);
// Output: 7625
```

Breaking it down step by step:

*   Start: `total = 0`
    
*   Step 1: `0 + 1200 = 1200`
    
*   Step 2: `1200 + 450 = 1650`
    
*   Step 3: `1650 + 3000 = 4650`
    
*   Step 4: `4650 + 875 = 5525`
    
*   Step 5: `5525 + 2100 = 7625`
    

The `0` at the end is the initial value of the accumulator. Always pass this in. Without it, `reduce` uses the first element as the starting value, which can cause hard-to-debug bugs on empty arrays.

### Conditional Methods — Every and Some

These test a condition against the array and return a boolean.

#### `every()`

Returns `true` only if every element passes the test. One failure and it's `false`.

```javascript
const formFields = ["Shravan", "shravan@example.com", "123 Main St"];

const allFilled = formFields.every((field) => field.trim() !== "");

console.log(allFilled);
// Output: true

const incompleteForm = ["Shravan", "", "123 Main St"];

const ready = incompleteForm.every((field) => field.trim() !== "");

console.log(ready);
// Output: false
```

#### `some()`

Returns `true` if at least one element passes the test.

```javascript
const cartItems = [
  { name: "Headphones", inStock: true },
  { name: "Webcam", inStock: false },
  { name: "Mousepad", inStock: true },
];

const hasOutOfStock = cartItems.some((item) => !item.inStock);

console.log(hasOutOfStock);
// Output: true
// The checkout button should be disabled or show a warning.
```

#### `find()`

Returns the first element that passes the condition. Returns `undefined` if nothing matches.

```javascript
const users = [
  { id: 101, name: "Aarav" },
  { id: 102, name: "Bhavna" },
  { id: 103, name: "Chirag" },
];

const user = users.find((u) => u.id === 102);

console.log(user);
// Output: { id: 102, name: "Bhavna" }

const missing = users.find((u) => u.id === 999);
console.log(missing);
// Output: undefined
```

#### `findIndex()`

Same as `find`, but returns the index instead of the element itself. Returns `-1` if not found.

```javascript
const products = ["Pen", "Notebook", "Eraser", "Ruler"];

const index = products.findIndex((p) => p === "Eraser");

console.log(index);
// Output: 2
```