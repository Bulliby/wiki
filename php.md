---
title: php
description: 
published: true
date: 2020-09-05T10:54:42.542Z
tags: 
editor: markdown
---

# Type Juggling

Type **juggling** is an *implicit cast* who appear when manipulating variables. Like PHP isn't explicitly typed implicit cast happen. The type of a variable is set in function of context of the variable.

##### Example of type juggling (on assignation):

```php
<?php

$boolean = true;
$integer = $boolean + 1;

echo gettype($boolean) . PHP_EOL; //boolean
echo gettype($integer) . PHP_EOL; //integer
```

##### String to numbrer :
```php
<?php

$string = "123Ma phrase";

$total = 10 + $string;
echo $total . PHP_EOL;//Warning & 133;
?>
```

###### (Type juggling on comparison):

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

## Comparison

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

## PHP Advertisement

On certain function we can find in the PHP's **documentation** an advertisement that the function can return **false** *or* a value that can be interpreted like *false* by PHP in a loosely comparison.

This is the case with the [reset](https://www.php.net/manual/fr/function.reset.php) function.

## Security

Type juggling or loose comparison don't expose the developer to security issue in general becasue the HTTP's input are always string. Nevertheless this can happen by JSON parsing of response or cookie. Check the reference.

## References
[type juggling](https://www.php.net/manual/fr/language.types.type-juggling.php) ; [security](https://www.php.net/manual/fr/language.types.type-juggling.php) ; [reset](https://www.php.net/manual/fr/function.reset.php)

## Notes
You can incrment a string

```php
	$string = 'deuw';
	echo ++$strig; //deux
```

> The `+=1` however throw a warning and change the type of the variable.

# Ternary operator

```php
	expr1 ?: expr3
```

> Return expr1 if expr1 is **true**

```php
	(expr1) ?? (expr2) 
```

> Since php7, return expr1 if different of **NULL**