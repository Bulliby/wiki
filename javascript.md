<!-- TITLE: Javascript -->
<!-- SUBTITLE: Some notes about the Javascript language -->

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
