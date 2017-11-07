# Advanced Selecting Readme

## Objectives

1. Learn about selecting multiple elements with document.querySelectorAll
2. Learn to select nested elements
2. Change the value of the correct DOM nodes

## Introduction

In this lab, we're going to practice finding specific elements in the DOM. Let's start off with a review of our `querySelector()`, which is immensely useful for navigating the DOM.

### `querySelector()`

As you have seen in the previous lesson, `querySelector()` takes one argument, a string of [selectors](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_Started/Selectors), and returns the first element that matches these selectors. For example, consider selecting the `h1` of our [Ada Lovelace Wikipedia entry](https://en.wikipedia.org/wiki/Ada_Lovelace):

``` js
document.querySelector('h1')
// <h1 id="firstHeading" class="firstHeading" lang="en">Ada Lovelace</h1>
```
> You can navigate to the page either by [clicking here](https://en.wikipedia.org/wiki/Ada_Lovelace) or opening the `index.html` file provided in  your browser that is provided in this lab.

### Selecting Multiple Elements

So far we saw `querySelector` which returns the first element that corresponds to the matching selector.  Well, we can also use `querySelectorAll`, a similar method that returns all elements that matches the passed in selector.   Just like our `querySelector` method, `querySelectorAll` accepts a selector as its argument, and it searches from the element that it's called on (or from `document`) -- but instead of returning the _first_ match, it returns a NodeList (which, remember, is _not_ an Array) of matching elements.

Let's see this is in action.  For example, let's say that we would like to get a sense of the outline of our Wikipedia article.  Well, HTML standards say that there should only be one `h1` on the page.  So what about an `h2`, which is just one step below in rank from an `h1`.  

```js
	let subheadings = document.querySelectorAll('h2')
	// [h2, h2, h2, h2, h2, h2, h2, h2, h2, h2, h2, h2, h2, h2, h2]
	
	subheadings.constructor
	// ƒ NodeList() { [native code] }
```

As you can see this selects all of the `h2` elements on the page and returns them in a NodeList.  As you may remember, a NodeList operates a lot like an array so we can retrieve the first element with a call to `subheadings[0]`, which returns the first selected element.  It would be nice to return an array of the text of all of the subheadings.  Because a NodeList in JavaScript does not respond to the `map` function, we first must coerce the NodeList into an array, and then map through the elements to return the text of each.

```js
let subheadings = document.querySelectorAll('h2')
// [h2, h2, h2, h2, h2, h2, h2, h2, h2, h2, h2, h2, h2, h2, h2]
Array.from(subheadings).map((heading) => heading.innerText)
// ["Contents", "Biography[edit]", "Work[edit]", "In popular culture[edit]", 
"Commemoration[edit]", "Titles and styles by which she was known[edit]", 
"Ancestry[edit]", "Bicentenary[edit]", "Publications[edit]", "See also[edit]", 
"Notes[edit]", "References[edit]", "Sources[edit]", "External links[edit]", 
"Navigation menu"]
```

### Selecting Nested Elements

Ok, so that wasn't bad, but it seems like a more careful way to get an outline of the page is simply to look at the elements inside of the gray table of contents box.  


We can make sure that we only select elements from the box, by first selecting the box, and then selecting the list elements inside of the gray box.  Here's how:

```js
let tableOfContents = document.querySelector('.toc')
let subheadings = tableOfContents.querySelectorAll('li')

// [li.toclevel-1.tocsection-1, li.toclevel-2.tocsection-2, 
li.toclevel-2.tocsection-3, li.toclevel-2.tocsection-4, 
li.toclevel-2.tocsection-5, li.toclevel-1.tocsection-6, 
...]
```

Ok, done and done.  Do you see why we selected these elements?  It's because we first selected the HTML `div` with the `class` of `toc`.  Then we selected the list elements inside of our this selected `div`.  Another way of doing this is to simply chain the method calls directly:

```js
let subheadings = document.querySelector('.toc').
	tableOfContents.querySelectorAll('li')

// [li.toclevel-1.tocsection-1, li.toclevel-2.tocsection-2, 
li.toclevel-2.tocsection-3, li.toclevel-2.tocsection-4, 
li.toclevel-2.tocsection-5, li.toclevel-1.tocsection-6, 
...]
```

### All together now

Now that we saw how we can select multiple elements, let's consider how to select nested elements just with one call to `querySelectorAll`.  For example consider the following method call: `document.querySelectorAll('table.biography a')`.  Now try to guess what that will return.  Just take a guess, it's more fun.  

Ok, so it returns the anchor elements inside of the table with a class of biography.  Do you see why?  Let's take our method call piece by piece.  The call to `document.querySelectorAll('table.biography a')` means find a `table` with a class of `biography`, then from that `table` find the anchor tags that are inside of that table: thus returning a Nodelist of the anchor tags that are inside of the box.  

That's the gist of selecting elements.  If you would like to read more, check out the following link about on [selectors](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_Started/Selectors). They're super important and relatively straightforward to pick up. Play around on the MDN page while you're getting the hang of it! Then come back when you're ready.

## Resources

- [document.querySelector()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)
- [document.querySelectorAll()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)
- [parseInt()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt)
- [Selectors](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_Started/Selectors)
