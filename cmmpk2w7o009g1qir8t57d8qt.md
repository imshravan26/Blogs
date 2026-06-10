---
title: "Control Flow in JavaScript: If, Else, and Switch Explained"
seoTitle: "Control Flow in JavaScript: If, Else, and Switch Explained"
seoDescription: "A beginner's guide to if, else, and switch. The three tools that let your JavaScript code think for itself."
datePublished: 2026-03-13T23:56:43.286Z
cuid: cmmpk2w7o009g1qir8t57d8qt
slug: control-flow-in-javascript-if-else-and-switch-explained
cover: https://cdn.hashnode.com/uploads/covers/6836cc7a1c8efb431960e9f0/dc5e2a81-0911-426f-9ab1-a7b3589ad22e.png
tags: javascript, switch-case, javascript-fundamentals, if-else, javascript-interview-question, control-flow, else-if

---

Every day, you make decisions without even thinking about it. You wake up and check the weather, if it is raining, you grab an umbrella. If it is not, you leave without one. You look at the time, if you are running late, you skip breakfast. Otherwise, you sit down and eat.

Programs work the same way. They reach a point where they need to decide: should I do this, or that? The mechanism that controls this is called **control flow**, and it is one of the most fundamental ideas in programming.

In JavaScript, the primary tools for handling control flow are the `if` statement, the `if-else` statement, the `else if` ladder, and the `switch` statement. Let's walk through each one.

## **What Is Control Flow?**

By default, JavaScript runs your code from top to bottom, one line at a time. Control flow is what lets you change that. To skip certain lines, repeat others, or take a completely different path depending on a condition.

### **The** `if` **Statement**

The `if` statement is the simplest form of decision-making. You give it a condition, and if that condition is true, it runs a block of code. If the condition is false, it just moves on.

```javascript
let age = 20;

if (age >= 18) {
  console.log("You are an adult.");
}
```

Here, JavaScript checks whether `age >= 18` is true. Since 20 is indeed greater than or equal to 18, the message prints. If age were 15, nothing would happen, the block would be skipped entirely.

The condition inside the parentheses always evaluates to either `true` or `false`. That result is what JavaScript uses to decide whether to enter the block or not.

### **The** `if-else` **Statement**

The plain `if` only acts when the condition is true. But what about when it is false? That is where `else` comes in. It gives you a fallback, a block that runs specifically when the condition does not hold.

```javascript
let marks = 45;

if (marks >= 50) {
  console.log("You passed.");
} else {
  console.log("You failed.");
}
```

Step by step: JavaScript checks whether `marks >= 50`. Since 45 is not greater than or equal to 50, the `if` block is skipped. The `else` block runs instead, and "You failed." is printed.

The `else` block has no condition of its own. It is simply the catch-all, whatever was not handled by the `if`.

### **The** `else if` **Ladder**

![](https://cdn.hashnode.com/uploads/covers/6836cc7a1c8efb431960e9f0/0b4ce9e0-5a74-41eb-9752-88cbd8bdf2fe.png align="center")

Sometimes two options are not enough. You might have three, four, or more distinct cases to handle. The `else if` ladder lets you chain multiple conditions together.

```javascript
let marks = 72;

if (marks >= 90) {
  console.log("Grade: A");
} else if (marks >= 75) {
  console.log("Grade: B");
} else if (marks >= 60) {
  console.log("Grade: C");
} else {
  console.log("Grade: D");
}
```

JavaScript goes through each condition from top to bottom. The moment it finds one that is true, it runs that block and skips everything else. Since 72 is not >= 90, the first block is skipped. It is not >= 75, so the second is skipped too. But 72 is >= 60, so "Grade: C" is printed, and the rest of the ladder is ignored.

This top-to-bottom, first-match-wins behavior is important to understand. If you put a broader condition above a narrower one, the narrower one might never get a chance to run.

### **The** `switch` **Statement**

![](https://cdn.hashnode.com/uploads/covers/6836cc7a1c8efb431960e9f0/5c08ebc5-e922-4f84-8e47-5fa71f7fe688.png align="center")

The `switch` statement is designed for a specific scenario: when you have one variable and you want to compare it against several exact values.

```javascript
let day = 3;

switch (day) {
  case 1:
    console.log("Monday");
    break;
  case 2:
    console.log("Tuesday");
    break;
  case 3:
    console.log("Wednesday");
    break;
  case 4:
    console.log("Thursday");
    break;
  case 5:
    console.log("Friday");
    break;
  default:
    console.log("Weekend");
}
```

`switch` takes an expression here, `day` and checks it against each `case`. When it finds a match (`case 3`), it starts executing from there.

Notice the `break` at the end of each case. That is not optional decoration. Without it, JavaScript does not stop after the matching case, it keeps running into the next case, and the one after that, until it either hits a `break` or reaches the end of the switch block. This behavior is called **fall-through**, and it trips up a lot of people early on.

The `default` at the bottom is the equivalent of `else`, it runs when none of the cases match.

### **When to Use** `switch` **vs** `if-else`

This is a practical question, and the honest answer is: most of the time, both will work. But they each have a natural home.

Use `if-else` when you are checking ranges or conditions that involve comparisons. Checking whether a number is greater than something, whether a string contains a value, whether two things are not equal, these are all range-based or logical checks that `if-else` handles naturally.

Use `switch` when you are checking a single variable against a fixed list of exact values. Days of the week, months of the year, user roles, status codes. These are cases where `switch` reads more cleanly and makes the intent obvious. When you see a `switch`, you immediately know: this variable is being compared to a set of known values.

There is also a readability argument. A `switch` with ten cases is generally easier to scan than an `else if` ladder with ten conditions. But a `switch` trying to handle range checks gets awkward fast, because cases only match exact values, not ranges.

## **Wrapping Up**

Control flow is not a complicated idea. At its core, it is just your program asking a question and acting on the answer. The `if` statement handles the simplest version of that, do this if the condition is true. `if-else` adds a fallback for when it is not. The `else if` ladder extends that into multiple branches. And `switch` gives you a cleaner way to handle the case where one variable maps to several known values.

These four tools will show up in virtually every JavaScript program you write. Not because they are advanced, but because decision-making is unavoidable. The moment your code needs to behave differently based on input, state, or any condition at all, you will reach for one of these.

Start with `if-else` for most things. Reach for `switch` when you find yourself writing the same variable name five times in a row across an `else if` ladder. And always remember the `break` inside switch, skipping it once will teach you why it matters.