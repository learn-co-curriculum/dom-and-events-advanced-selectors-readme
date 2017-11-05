# Advanced Selecting Readme

## Objectives

1. Learn about selecting multiple elements with document.querySelectorAll
2. Learn to select nested elements
2. Change the value of the correct DOM nodes

## Introduction

In this lab, we're going to practice finding specific elements in the DOM. Let's start off with a review of our `querySelector()`, which is immensely useful for navigating the DOM.

### `querySelector()`

As you have seen in the previous lesson, `querySelector()` takes one argument, a string of [selectors](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_Started/Selectors), and returns the first element that matches these selectors. For example, consider the following document:

``` html
<body>
  <div>
    Hello!
    <p> And welcome to a new day.</p>
  </div>

  <div>
    Goodbye!
  </div>
</body>
```

If we called `document.querySelector('div')`, the method would return the first `div` (with the text "Hello!" inside, along with the `p` tag saying "And welcome to a new day").

### Selecting Multiple Elements

So far we saw `querySelector` which returns the first element that corresponds to the matching selector.  Well, we can also use `querySelectorAll`, a similar method that returns all elements that matches the passed in selector.   Just like our `querySelector` method, `querySelectorAll` accepts a selector as its argument, and it searches from the element that it's called on (or from `document`) -- but instead of returning the _first_ match, it returns a NodeList (which, remember, is _not_ an Array) of matching elements.

Let's see this is in action.  Consider the following HTML:

``` html
<div id="app">
  <ul class="bright-colors">
    <li>pink</li>
    <li>yellow</li>
  </ul>

  <ul class="lower-list">
    <li>blue</li>
    <li>green</li>
  </ul>
</div>
<div id="footer">
  <ul>
     <li>A special production</li>
  </ul>
</div>

```

If we called `document.getElementById('#app').querySelectorAll('li')`, we'd get back a NodeList of `<li>pink</li>, <li>yellow</li>, <li>blue</li>, <li>green</li>`.  Note that the list element with the text "A special production" is not selected.  You can see that if we take a look at the text of each of the selected list elements.

```js
let selectedLis = document.getElementById('app').querySelectorAll('li')
// [li, li, li, li]
Array.from(selectedLis).map((li) => li.innerText)
// ["pink", "yellow", "blue", "green"]
```
> Note: Remember when that when we select the elements we return a NodeList which does not have the map method, so we must first convert the NodeList to an array by using Array.from.

Do you see why we selected these elements?  It's because we first selected the HTML elements that included in our `div` with the `id` of `app`.  So this did not include the second `div` with an `id` of `footer`.  Then we selected the list elements inside of our `div` with the `id` app.  Thus we selected the first four list elements.

```js
document.querySelector('#app')
<div id="app">
  <ul class="bright-colors">
    <li>pink</li>
    <li>yellow</li>
  </ul>

  <ul class="lower-list">
     <li>blue</li>
     <li>green</li>
   </ul>
</div>
```

### Selecting Nested Elements

Now that we saw how we can select multiple elements, let's consider how to select nested elements just with one call to `querySelectorAll`.  For example consider the following method call: `document.querySelectorAll(ul.bright-colors li)`.  Now try to guess what that will return.  Just take a guess, it's more fun.  

Ok, so it returns the list elements with the text of `blue` and `green`.  Do you see why?  Let's take our method call piece by piece.  The call to `document.querySelectorAll('ul.ranked-list li')` means find a `ul` with a class of `ranked-list`, then from that ul find the lis that are nested inside: thus returning a Nodelist of the list elements that have text `blue` and `green`, respectively.  

That's the gist of selecting elements.  If you would like to read more, check out the following link about on [selectors](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_Started/Selectors). They're super important and relatively straightforward to pick up. Play around on the MDN page while you're getting the hang of it! Then come back when you're ready.

## Resources

- [document.querySelector()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)
- [document.querySelectorAll()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)
- [parseInt()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt)
- [Selectors](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_Started/Selectors)
