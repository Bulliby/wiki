---
title: Javascript
description: Some notes about the Javascript language
published: true
date: 2021-04-21T18:54:14.380Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:58:29.800Z
---

# Javascript

## Promise

> A Promise is an object representing the eventual completion or failure of an asynchronous operation. Since most people are consumers of already-created promises, this guide will explain consumption of returned promises before explaining how to create them.

### Creation

We can create a **Promise** who handle a async request like this :
```js
var promise1 = new Promise(function(resolve, reject) {
  setTimeout(function() {
    resolve('foo');
  }, 300);
});
```

The **resolve** function permit to return the **new** Promise. We can now chain it with the **then** keyword.

If we have an utility like *axios* with a `.get` function who return a **Promise**, we can use it like this :

```js
  axios
  .get('http://www.google.fr')
  .then((result) => { console.log('data-fetched is :' + result ); })
```

### All

`Promise.all()` permit to execute several async request and store their results in array :

```js
 Promise.all(pall1).then((values) => { console.log('array of the resulted promise are stored in values' ) });
```

## Scope


The scope in *JS* is not like in C who is **block scoped**  here the code is **function scoped** or global. If we want to trix and have a scope in a if statements we can define a *auto-called* function who contain the code we want block scoped, like this :

```js
if (true)
{
  (function() {
    var x;
    x = "Like this my variable x is not accessible out of if statement";
  })();
  //Not present here neither. Js is function scoped...
}
//Not accessible here.
```

## Hoisting

We name **hoisting** the fact that *javascript* take the declaration variables before execution and put them at the top of the current scope. By the way this two snippet are identical :

```js
x = "test";
console.log(x);
var x;
```

```js
var x;
x = test;
console.log(x);
```

They don't take the definition, when any, at the time of declaration, so :

```js
foo();
var foo = function () {};
```

will result on the following error : `TypeError: foo is not a function`.
