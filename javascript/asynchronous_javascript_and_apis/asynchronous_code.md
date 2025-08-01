### Introduction

Since JavaScript is the language of the web, there are some functions that by necessity are going to take a decent amount of time to complete, such as fetching data from a server to display on your site.  For this reason, JavaScript includes support for asynchronous functions, or to put it another way, functions that can happen in the background while the rest of your code executes.

### Lesson overview

This section contains a general overview of topics that you will learn in this lesson.

- Explain what a callback is.
- Explain what a promise is.
- Explain the circumstances under which promises are better than callbacks.
- Explain what the `.then()` function does.

### Callbacks

In the recent past, the way that these were most commonly handled were with **callbacks**, and even now they are still used quite a lot in certain circumstances.

A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action ([MDN documentation on callback functions](https://developer.mozilla.org/en-US/docs/Glossary/Callback_function)).

Callbacks are functions that get passed into other functions. For example:

```javascript
myDiv.addEventListener("click", function(){
  // do something!
})
```

Here, the function `addEventListener()` takes a callback (the "do something" function) and then calls it when `myDiv` gets clicked.

You will likely recognize this pattern as something that happens *all the time* in JavaScript code.  Unfortunately, though they are useful in situations like the above example, using callbacks can get out of hand, especially when you need to chain several of them together in a specific order.  The rest of this lesson discusses patterns and functions that will help keep you out of Callback hell.

Take a moment to read the section on callbacks in [this article](https://github.com/maxogden/art-of-node#callbacks) before moving on.  Or, if you prefer to watch a video of [Callback functions](https://www.youtube.com/watch?v=QRq2zMHlBz4).

### Promises

There are multiple ways that you can handle asynchronous code in JavaScript, and they all have their use cases.  Promises are one such mechanism, and they're one you will see somewhat often when using other libraries or frameworks.  Knowing what they are and how to use them is quite useful.

Essentially, a promise is an object that might produce a value at some point in the future.  Here's an example:

Lets say `getData()` is a function that fetches some data from a server and returns it as an object that we can use in our code:

```javascript
const getData = function() {
  // go fetch data from some API...
  // clean it up a bit and return it as an object:
  return data
}
```

The issue with this example is that it takes some time to fetch the data, but unless we tell our code that, it assumes that everything in the function happens essentially instantly.  So, if we try to do this:

```javascript
const myData = getData()
const pieceOfData = myData['whatever']
```

We're going to run into trouble because when we try to extract `pieceOfData` out of the returned data, the function `getData()` will most likely still be fetching, so `myData` will not be the expected data, but will be `undefined`.  Sad.

We need some way to solve this problem, and tell our code to wait until the data is done fetching to continue.  Promises solve this issue.  We'll leave learning the specific syntax for the articles you're about to read, but essentially Promises allow you to do this:

```javascript
const myData = getData() // if this is refactored to return a Promise...

myData.then(function(data){ // .then() tells it to wait until the promise is resolved
  const pieceOfData = data['whatever'] // and THEN run the function inside
})
```

Of course, there are many more occasions where one would want to use Promises beyond fetching data, so learning these things now will be very useful to you.

### Assignment

<div class="lesson-content__panel" markdown="1">

1. Read this [Promises article](https://davidwalsh.name/promises). It's a good starting place and it's short and to the point.
1. Watch this [video about promises](https://youtu.be/DHvZLI7Db8E).  It's a good place to get a feel for how one might actually use promises in the wild.
1. Watch this [video titled "What is Event Loop?"](https://www.youtube.com/watch?v=8aGhZQkoFbQ) to understand how asynchronous code works in JavaScript.
1. Watch this [video visualizing the Event loop](https://www.youtube.com/watch?v=eiC58R16hb8) to further understand the Event Loop.
1. Watch this [video visualizing promises](https://www.youtube.com/watch?v=Xs1EMmBLpn4) to understand Promise Execution in JavaScript.
1. Read this [promise basics article](https://javascript.info/promise-basics), which is an excellent resource for beginners.

</div>

### Knowledge check

The following questions are an opportunity to reflect on key topics in this lesson. If you can't answer a question, click on it to review the material, but keep in mind you are not expected to memorize or master this knowledge.

- [What is a callback?](https://developer.mozilla.org/en-US/docs/Glossary/Callback_function)
- [What is a promise?](#promises)
- [When should you use promises over callbacks?](http://callbackhell.com/)
- [What does the `.then()` function do?](https://davidwalsh.name/promises)

### Additional resources

This section contains helpful links to related content. It isn't required, so consider it supplemental.

- The [Promises by ColorCode video](https://www.youtube.com/watch?v=TnhCX0KkPqs) is a nice introduction to Promises if you need additional information.
- For a more interactive explanation and example, try a [Scrim on asynchronous coding](https://scrimba.com/scrim/cof4e4fb797a2d0a236ea38ce?embed=odin,mini-header,no-next-up).
- Read ["You Don't Know JavaScript" Chapter 2: Callbacks](https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/async%20%26%20performance/ch2.md) and [Chapter 3: Promises](https://github.com/getify/You-Dont-Know-JS/blob/1st-ed/async%20%26%20performance/ch3.md). Both chapters dive deep into their respective topics, which may make for a difficult - but worthwhile - read.
