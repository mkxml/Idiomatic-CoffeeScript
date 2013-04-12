Idiomatic-CoffeeScript
======================

Purpose
-------

Idiomatic CoffeeScript is a set of best practices in CoffeeScript programming. This project is inspired
in Idiomatic JavaScript by @rwldrn.

So this also serve as a programming style guide, which is useful for team development,
so everyone can code in the same manner.

As said on the Idiomatic JavaScript: "All code in any code-base should look like a single person typed it, no matter how many people contributed.",
and that's absolutely true. So this guide purpose is to apply that concept in CoffeeScript codes.

Important: In order to make this guide simple to follow it doesn't offer options and paths as the Idiomatic JavaScript does, if you want you can
fork this guide and customize it to fit your tools and style.

How to use
----------

Link this document refering it as the style guide for your project, so anyone know how you code.
The styling guide should be the first thing you define in your project, after it is done everything must be based on it.

Style guide
===========

Basics
------

1. Regarding line writing
	- Use 2 spaces to indent, you can also convert tabs into 2 spaces (Sublime Text 2 and other code editors allows this);
	- The maximum line length is 72 characters;
	- Don't leave trailing spaces;
	- Use one blank line to separate functions;
  - Leave one blank line at the end of the code;
	- Don't use blank lines to separate lines within the same function.

Example:
	
  ```coffeescript

  add = (num1, num2) ->
    num1 + num2

  result = add 1,2

  #Breaking line because string has more than 72 characters
  string = "We performed a sum between 1 and 2 and the result
   is #{result}"

  ```