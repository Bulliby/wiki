---
title: Eloquent-book
description: 
published: true
date: 2021-04-21T18:56:02.237Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:58:14.759Z
---

# Eloquent Javascript Book

## Chapter 1 (Values, Types and Operators)

* Javascript use 16 bits per string elements wich can describe 2^16 characters. Unicode table describe about twice more so some characters like **emoji** take up two character positions in javascript.

*  Operator precedence :
`||` as the lower precedence, then `&&` and after comparison operators `== <= > ...` and the others operators.

* If you don't want automatic type conversion when you do comparison. You use `===` or `!==`.

* Short circuiting evaluation. `false || true` give `true`, `false && true` give `true`. This permit the same things as **Ternary Operator**.

## Chapter 2 (Program Structure)

* **expression** is a fragment of text who produce a value.

* **bindings** : When a binding points at a value, that does not mean it is tied to that value forever. The = operator can be used at any time on existing bindings to disconnect them from their current value and have them point to a new one.

## Chapter 3 (Functions)

* In **pre-2015 JavaScript**, only functions created new scopes, so old-style bindings, created with
the var keyword, are visible throughout the whole function that they appear in—or throughout the global scope, if they are not in a function.

* Each scope can `look out` into the scope around it.

* Each local scope can also see all the local scopes that contain it, and all scopes can see the global scope. This approach to binding visibility is called **lexical scoping**.

* **Closure** :

```javascript
  function multiplier(factor) {
    return number => number * factor;
  }
  let twice = multiplier(2);
  console.log(twice(5));
  // → 10
```

* Functions can be roughly divided into those that are called for their **side effects** and those that are called for their **return value**.

* A pure function is a specific kind of value-producing function that not only has no side effects but also doesn’t rely on side effects from other code—for example, it doesn’t read global bindings whose value
might change.

## Chapter 4 (Data Structures: Objects and Arrays)

* Numbers, strings, and Booleans, are all immutable—it is impossible to change values of those types. We can change there bindings or derive them but we can't change their intrinsic value.

* **Destructuring**

```Javascript
  let array = ["TOTO", "TATA", "TUTU"];

  function test([toto, tata, tutu]) {
    console.log(toto); //TOTO
    console.log(tata); //TATA
    console.log(tutu); //TUTU
  }
  test(array);
```

## Chapter 5 (Higher-order functions)

* Functions that operate on other functions, either by taking them as arguments or by returning them, are called **higher-order functions**.

