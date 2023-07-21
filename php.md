---
title: php
description: 
published: true
date: 2023-07-21T17:41:37.860Z
tags: 
editor: markdown
dateCreated: 2021-03-30T19:58:40.876Z
---

# PHP

## Type Juggling

**Type juggling** is an *implicit cast* who appear when manipulating variables. We encounter it in PHP, Javascript.. The type of a variable is "guessed" accordingly to context.

### Example of type juggling (on assignation):

```php
<?php

$boolean = true;
$integer = $boolean + 1;

echo gettype($boolean) . PHP_EOL; //boolean
echo gettype($integer) . PHP_EOL; //integer
```

### String to numbrer :
```php
<?php

$string = "123Ma phrase";

$total = 10 + $string;
echo $total . PHP_EOL;//Warning & 133;
?>
```

### Type juggling on comparison :

```php
<?php

if ("0" == false)//TRUE
    echo "TRUE";
else
    echo "FALSE";

if ("123" == 123)//TRUE
    echo "TRUE";
else
    echo "FALSE";
?>
```

Here an `implicit cast` have been made before comparison who transform string in integer.

### Comparison

There is two type of comparison **loose** and **strict** one. Loose are comparison who *doesn't care* of the variable's **type**. Strict one check *type and value*.

```php
<?php

if ("0" === false)//FALSE
    echo "TRUE";
else
    echo "FALSE";

if ("123" === 123)//FALSE
    echo "TRUE";
else
    echo "FALSE";
?>
```

We can see that we can **mitigate** the result of precedent test with **strict** comparison.

### PHP Advertisement

On certain function we can find in the PHP's **documentation** an advertisement that the function can return **false** *or* a value that can be interpreted like *false* by PHP in a loosely comparison.

This is the case with the [reset](https://www.php.net/manual/fr/function.reset.php) function.


### References
* [type juggling](https://www.php.net/manual/fr/language.types.type-juggling.php) 
* [security](https://www.php.net/manual/fr/language.types.type-juggling.php)
* [reset](https://www.php.net/manual/fr/function.reset.php)

### Notes

You can incrment a string

```php
	$string = 'deuw';
	echo ++$strig; //deux
```

## Ternary operator

```php
	expr1 ?: expr3
```

> Return expr1 if expr1 is **true**

```php
	(expr1) ?? (expr2) 
```

> Equivalent to `isset($expr1) ? $expr1 : null`