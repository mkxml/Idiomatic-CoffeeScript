# Idiomatic-CoffeeScript

## Purpose

Idiomatic CoffeeScript is a set of best practices in CoffeeScript programming. This project is inspired
in Idiomatic JavaScript by @rwldrn.

So this also serve as a programming style guide, which is useful for team development,
so everyone can code in the same manner.

As said on the Idiomatic JavaScript: "All code in any code-base should look like a single person typed it, no matter how many people contributed.",
and that's absolutely true. So this guide purpose is to apply that concept in CoffeeScript codes.

Important: In order to make this guide simple to follow it doesn't offer options and paths as the Idiomatic JavaScript does, if you want you can
fork this guide and customize it to fit your tools and style.

## How to use

Link this document refering it as the style guide for your project, so anyone know how you code.
The styling guide should be the first thing you define in your project, after it is done everything must be based on it.

## Style guide

### How to code better

1. Regarding line writing:
	* Use 2 spaces to indent, you can also convert tabs into 2 spaces (Sublime Text 2 and other code editors allows this);
	* The maximum line length is 72 characters;
	* Don't leave trailing spaces;
	* Use one blank line to separate functions;
  * Leave one blank line at the end of the code;
	* Don't use blank lines to separate lines within the same function.

2. Regarding string usage:
  * Always use double quotes in strings;
  * Break long strings, CoffeeScript supports multi-line strings;
  * Use CoffeeScript string interpolation instead of concatenation.

3. Regarding comments:
  * Use single line (#) comments most of the time;
  * Just use multi line comments (###) on the header which contains information about the file.

Example:
	
  ```coffeescript

  add = (num1, num2) ->
    num1 + num2

  result = add 1,2

  #Breaking line because string has more than 72 characters
  string = "We performed a sum between 1 and 2 and the result
   is #{result}"

  ```

3. Use CoffeeScript peculiarities on your favor
  * Make use of the implicit return syntax in your projects;
  * When you have to pass a variable number of arguments to a function, use splats;
  * Instead of executing simple functions in loops use object or array comprehensions;
  * Don't use object or array comprehensions for complex stuff, it makes it hard to read;
  * Make use of closures created with ```do``` when building your modules;
  * Don't use parenthesis in function calls unless completely necessary;
  * Use CoffeeScript boolean's flexibility to improve readability;
  * Don't use commas when writing long literal array and object notations, instead, add line breaks at each node.


Example:

  ```coffeescript
  #Using closure, you can add parameters here as well
  do ->
    
    #Array declaration without commas
    pilots = [
      "Senna"
      "Alonso"
      "Schumacher"
      "Vettel"
      "Hamilton"
      "Barichello"
    ]

    #Sample podium function, showing how you can use splats,
    #string line breaks, string interpolation and implicit return
    podium = (fisrt, second, third, rest...) ->
      "Gold Trophy: #{first}, Silver trophy: #{silver}, Bronze trophy:
       #{bronze}. Contenders: #{rest.join ","}"
    
    #Calling a function with splats
    podium pilots...

    #A more friendly aproach to boolean values.
    #No need to use splats here, I just use to reuse the elements I
    #already had.
    didSennaWin = (first, pilots...) ->
      if first is "Senna" then yes else no

  ```
