---
title: "CSS Selectors 101: Targeting Elements with Precision"
seoTitle: "CSS Selectors Guide: Master Element Targeting"
seoDescription: "Learn how to use CSS selectors to precisely target and style HTML elements on your web pages with ease"
datePublished: 2026-02-15T18:18:19.150Z
cuid: cmlo2jk3y000d02l5bspq63tl
slug: css-selectors-101-targeting-elements-with-precision
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1771179441414/2781f56a-378b-4c32-8f50-8f9a41ca27f3.png
tags: css3, css, selectors, cssselector, css-basics

---

When you start learning CSS, one of the first things you need to understand is how to tell the browser which elements you want to style. This is where CSS selectors come in. Think of selectors as a way to point at specific parts of your webpage and say "I want to change this."

## Why Do We Need CSS Selectors?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771179387492/13dbd5ce-58c4-4dfd-97df-3879f1065daa.png align="center")

Imagine you have a webpage with hundreds of paragraphs, dozens of headings, and many images. You want to make all your headings blue, but only some paragraphs should have a red background, and one specific image needs a border. How do you tell CSS which element to style?

This is exactly why we need selectors. Without selectors, you would have no way to apply styles to specific elements. Selectors are like addresses that help CSS find the right elements on your page.

Let me give you a real world analogy. Imagine you are in a large classroom and you want to give instructions to specific students. You could say "everyone wearing a red shirt, stand up" or "the person sitting in the front row, raise your hand" or "John, please come here." Each of these is a different way of selecting people, just like CSS selectors help you choose elements.

## Element Selector

The element selector is the most basic type of selector. It targets all elements of a specific HTML tag.

css

```css
p {
  color: blue;
}
```

This selector will make all paragraph text blue. If you have 50 paragraphs on your page, all of them will turn blue.

Here is another example:

css

```css
h1 {
  font-size: 32px;
  color: green;
}
```

This targets every h1 heading on your page and makes them 32 pixels in size and green in color.

**Before styling:**

html

```html
<h1>Welcome to My Website</h1>
<p>This is a paragraph.</p>
<p>This is another paragraph.</p>
```

The text appears in default black color with default sizes.

**After styling:**

css

```css
h1 {
  color: green;
  font-size: 32px;
}

p {
  color: blue;
}
```

Now the h1 is large and green, while both paragraphs are blue.

The element selector is useful when you want consistent styling across all instances of an element, but sometimes you need more control.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771179325902/df4956db-cf81-4be5-b307-2d4fd3040452.png align="center")

## Class Selector

What if you want to style only some paragraphs differently, not all of them? This is where the class selector becomes useful.

A class is like a label you can attach to any HTML element. You can use the same class on multiple elements, and you can even put multiple classes on one element.

In your HTML, you add a class using the class attribute:

html

```html
<p class="highlight">This paragraph is special.</p>
<p>This is a regular paragraph.</p>
<p class="highlight">This paragraph is also special.</p>
```

In your CSS, you target a class by putting a dot before the class name:

css

```css
.highlight {
  background-color: yellow;
  font-weight: bold;
}
```

Now only the paragraphs with the class "highlight" will have a yellow background and bold text. The regular paragraph stays unchanged.

Classes are reusable. You can apply the same class to different types of elements:

html

```html
<p class="highlight">A highlighted paragraph.</p>
<div class="highlight">A highlighted div.</div>
<span class="highlight">A highlighted span.</span>
```

All three will get the same styling.

**Before styling:**

html

```html
<p class="important">Read this carefully.</p>
<p>This is normal text.</p>
<p class="important">This is also important.</p>
```

All paragraphs look the same.

**After styling:**

css

```css
.important {
  color: red;
  border-left: 4px solid red;
  padding-left: 10px;
}
```

The paragraphs with class "important" now have red text and a red left border, while the normal paragraph remains unchanged.

## ID Selector

Sometimes you need to style one specific element that appears only once on your page. For this, you use an ID selector.

An ID is similar to a class, but with one major difference. Each ID should be unique on a page. You should only use a specific ID once.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771179344789/bdbd9bca-b5e6-44ef-b758-9ec24bf7b694.png align="center")

In HTML:

html

```html
<div id="header">This is the main header.</div>
<div>This is a regular div.</div>
<div>Another regular div.</div>
```

In CSS, you target an ID by putting a hash symbol before the ID name:

css

```css
#header {
  background-color: navy;
  color: white;
  padding: 20px;
}
```

Only the div with id "header" will get this styling.

Think of IDs like your social security number or student ID. Only one person has that specific number. Classes are more like job titles or club memberships. Many people can have the same title or belong to the same club.

**When to use class vs ID:**

Use a class when you might want to apply the same style to multiple elements. Use an ID when you are styling something unique like your main navigation bar, footer, or logo container.

## Group Selectors

Sometimes you want to apply the same styles to multiple different elements. Instead of writing the same CSS rules multiple times, you can group selectors together.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771179369595/98493c90-bdd0-441c-a638-08369e04d473.png align="center")

Without grouping:

css

```css
h1 {
  color: purple;
  font-family: Arial;
}

h2 {
  color: purple;
  font-family: Arial;
}

h3 {
  color: purple;
  font-family: Arial;
}
```

This is repetitive. Instead, you can group them:

css

```css
h1, h2, h3 {
  color: purple;
  font-family: Arial;
}
```

You separate each selector with a comma. This tells CSS to apply the same rules to all h1, h2, and h3 elements.

You can group any type of selector, not just element selectors:

css

```css
.header, #main-title, p {
  margin-bottom: 20px;
}
```

This applies a bottom margin to elements with class "header," the element with id "main-title," and all paragraph elements.

**Before styling:**

html

```html
<h1>Main Heading</h1>
<h2>Subheading</h2>
<h3>Minor Heading</h3>
```

All have different default sizes but the same black color.

**After styling:**

css

```css
h1, h2, h3 {
  color: darkblue;
  font-family: Georgia;
}
```

All three heading levels now share the same color and font, while keeping their individual size differences.

## Descendant Selectors

Descendant selectors let you target elements that are inside other elements. This is useful when you want to style something only when it appears in a specific context.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771179410922/b6eb5828-855b-4109-8c6f-8b3a2da7ccf3.png align="center")

html

```html
<div class="article">
  <p>This paragraph is inside the article.</p>
</div>

<p>This paragraph is outside the article.</p>
```

If you want to style only paragraphs that are inside the article div, you use a descendant selector:

css

```css
.article p {
  font-style: italic;
}
```

Notice the space between ".article" and "p". This space is important. It means "select all p elements that are descendants of elements with class article."

The paragraph inside the div with class "article" will be italic, but the paragraph outside will remain normal.

Descendant selectors can go multiple levels deep:

html

```html
<div class="container">
  <div class="content">
    <p>This is deeply nested.</p>
  </div>
</div>
```

css

```css
.container .content p {
  color: green;
}
```

This targets paragraphs inside elements with class "content," which are themselves inside elements with class "container."

**Before styling:**

html

```html
<nav>
  <a href="#">Home</a>
  <a href="#">About</a>
</nav>

<div class="content">
  <a href="#">Article Link</a>
</div>
```

All links look the same.

**After styling:**

css

```css
nav a {
  color: white;
  background-color: blue;
  padding: 10px;
}
```

Only the links inside the nav element get the blue background and white text. The link in the content div stays unchanged.

## Basic Selector Priority

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1771179431591/08d4984a-c25a-4618-a1aa-eeb33162b5b8.png align="center")

When you have multiple CSS rules targeting the same element, which one wins? CSS has a system called specificity that determines this.

Here is a simple way to think about it, from most specific to least specific:

1. ID selectors are the most specific
    
2. Class selectors are in the middle
    
3. Element selectors are the least specific
    

html

```html
<p id="special" class="text">Hello World</p>
```

css

```css
p {
  color: blue;
}

.text {
  color: green;
}

#special {
  color: red;
}
```

What color will "Hello World" be? It will be red, because the ID selector has the highest priority. Even though all three rules apply to this paragraph, the ID selector wins.

If you remove the ID:

html

```html
<p class="text">Hello World</p>
```

The text would be green, because the class selector beats the element selector.

If you remove both the ID and class:

html

```html
<p>Hello World</p>
```

The text would be blue, because only the element selector applies.

This priority system helps you understand why sometimes your CSS does not seem to work. If you style an element with a class but nothing happens, check if there is an ID selector somewhere else overriding your class styles.

**General rule:** Use element selectors for broad, page-wide styles. Use classes for reusable styles that apply to multiple elements. Use IDs sparingly for unique elements that appear only once.

## Wrapping Up

CSS selectors are the foundation of styling web pages. They let you precisely target elements and apply styles exactly where you want them. Understanding selectors well will make your CSS journey much smoother.

Start with the basics: element selectors for general styling, classes for reusable styles, and IDs for unique elements. As you practice, using descendant selectors and grouping selectors will become second nature.

The key is to practice. Create simple HTML pages and experiment with different selectors. Try combining them, see what works, and notice how specificity affects your styles. The more you practice, the more confident you will become in targeting elements with precision.

Remember, selectors are just the beginning. Once you master them, you will be ready to explore more advanced CSS concepts and create beautiful, well-styled websites.