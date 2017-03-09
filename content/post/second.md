+++
date        = "2013-06-21T11:27:27-04:00"
title       = "Second Post"
description = "Second Post description"
tags        = [ "Development", "Go", "profiling" ]
topics      = [ "Development", "Go" ]
slug        = "nitro"
+++

[![](http://farm1.static.flickr.com/104/308974073_9057064747_m.jpg "speed machine")](http://www.flickr.com/photos/fleur-design/308974073/) Nearly every website on the internet uses javascript in some form or fashion. Yet very few people, even those who write it and teach it, have a clear understanding of how javascript works!

Logical Operators are a core part of the language. We’re going to look at what logical operators are, what “truthy” and “falsy” mean, and **how to use this to write cleaner, faster and more optimized javascript**.

## Javascript Logical Operators

In traditional programming, operators such as `&&` and `||` returned a boolean value (`true` or `false`). This is not the case in javascript. Here it returns the actual `object`, not a `true` / `false`. To really explain this, I first have to explain what is truthy and what is falsy.

### Truthy or Falsy

When javascript is expecting a `boolean` and it’s given something else, it decides whether the something else is “truthy” or “falsy”.

An empty string (`''`), the number `0`, `null`, `NaN`, a boolean `false`, and `undefined` variables are all “falsy”. Everything else is “truthy”.

```
var emptyString = ""; // falsy

var nonEmptyString = "this is text"; // truthy

var numberZero = 0; // falsy

var numberOne = 1; // truthy

var emptyArray = []; // truthy, BUT []==false is true. More below.

var emptyObject = {}; // truthy

// NaN is a special javascript object for "Not a Number".
var notANumber = 5 / "tree"; // falsy

function exampleFunction(){
    alert("Test");
}

// examleFunction is truthy
// BUT exampleFunction() is falsy because it has no return (undefined)

```

Gotchas to watch out for: the strings `"0"` and `"false"` are both considered truthy. You can convert a string to a number with the `parseInt()` and `parseFloat()` functions, or by just multiplying it by `1`.

```
var test = "0"; // this is a string, not a number

var a = (test == false); // a is false, meaning that test is truthy

var b = (test * 1 == false); // b is true, meaning that `test * 1` is falsy

```

`Array`s are particularly weird. If you just test it for truthyness, an empty array is truthy. HOWEVER, if you compare an empty array to a boolean, it becomes falsy:

```
if ( [] == false ) {
    // this code runs
}

if ( [] ) {
    // this code also runs
}

if ([] == true) {
    // this code doesn't run
}

if ( ![] ) {
    // this code also doesn't run
}

```

(This is because when you do a comparison, it's elements are turned to `String`s and joined. Since it's empty, it becomes `""` which is then falsy. Yea, [it's weird](https://www.destroyallsoftware.com/talks/wat).)

If you write any PHP, then there's an additional gotcha to watch out for: while javascript evaluates empty arrays as true, PHP evaluates them as false.

PHP also evaluates “0″ as falsy. (However the string “false” is evaluated as truthy by both PHP and javascript.)

### How Logical Operators Work

#### Logical OR, `||`

The logical OR operator, `||`, is very simple after you understand what it is doing. If the first object is truthy, that gets returned. Otherwise, the second object gets returned.

```
var a = ("test one" || "test two"); // a is "test one"

var b = ("test one" || ""); // b is "test one"

var c = (0 || "test two"); // c is "Test two"

var d = (0 || false); // d is false

```

Where would you ever use this? The OR operator allows you to easily specify default variables in a function.

```
function sayHi(name){
    name = name || "Dave";
    alert("Hi " + name);
}

sayHi("Nathan"); // alerts "Hi Nathan";

sayHi(); // alerts "Hi Dave", name is set to null when the function is started

```

#### Logical AND, `&&`

The logical AND operator, `&&`, works similarly. If the first object is falsy, it returns that object. If it is truthy, it returns the second object.

```
var a = ("test one" && "test two"); // a is "test two"

var b = ("test one" && ""); // b is ""

var c = (0 && "test two") // c is 0

```

The logical AND allows you to make one variable dependent on another.

```
var checkbox = document.getElementById("agreeToTerms");

var name = checkbox.checked && prompt("What is your name");

// name is either their name, or false if they haven't checked the AgreeToTerms checkbox

```

#### Logical NOT, `!`

Unlike `&&` and `||`, the `!` operator DOES turn the value it receives into a boolean. If it receives a truthy value, it returns `false`, and if it receives a falsy value, it returns `true`.

```
var a = (!"test one" || "test two"); // a is "test two"
// ("test one" gets converted to false and skipped)

var b = (!"test one" && "test two"); // b is false
// ("test one" gets converted to false and returned)

var c = (!0 || !"test two"); // c is true
// (0 gets converted to true and returned)

```

Another useful way to use the `!` operator is to use two of them – this way you always get a `true` or a `false` no matter what was given to it.

```
var a = (!!"test"); // a is true
//  "test" is converted to false, then that is converted to true

var b = (!!""); // b is false
// "" is converted to true, and then that true is converted to false

var c = (!!variableThatDoesntExist); // c is false even though you're checking an undefined variable.

```

## [Javascript Optimization](http://nfriedly.com/portfolio)

Need any help [optimizing the Javascript and AJAX on your website](http://nfriedly.com/portfolio#javascript)? Get in touch with your friendly neighborhood [javascript expert](http://nfriedly.com/portfolio) for ideas on how to optimize your site and a free quote.
