# Idiomatic CoffeeScript - Normal version

## Purpose

Idiomatic CoffeeScript is a set of best practices in CoffeeScript programming. This project is inspired
in [Idiomatic JavaScript](https://github.com/rwaldron/idiomatic.js/) by [@rwaldron](https://github.com/rwaldron).

This also serve as a programming style guide, which is useful for team development,
so everyone can code in the same fashion.

As said on the Idiomatic JavaScript document: "All code in any code-base should look like a single person typed it, no matter how many people contributed",
and that's absolutely true. So this guide's purpose is to apply that concept in CoffeeScript as well.

Important: In order to make this guide simple to follow it doesn't offer options and paths as the Idiomatic JavaScript does, if you want to create new rules or change stuff you can
fork this guide and customize it to fit your tools and style.

## How to use

Link this document mentioning it as the style guide for your project, so everybody know how you code.
The styling guide should be the first thing you define in your project, after it is done everything must be based on it.

You can also link directly to the [strict version](https://github.com/mkautzmann/Idiomatic-CoffeeScript/tree/strict) of this document which introduces a more strict style of writing.

## Remember what CoffeeScript is

Always remember: CoffeeScript is just JavaScript. It is not an entirely new language, it is just a cool tool you can use to improve productivity and the readability of your code.
You should use it wisely otherwise you could end up generating terrible JS. This guide will help you get an idea of the path you need to follow to get the most out of CoffeeScript.

Reading [this article](https://github.com/raganwald/homoiconic/blob/master/2011/12/jargon.md) is strongly recommended to get an idea on what CoffeeScript is. Also, this guide assumes that you already know you to use CoffeeScript. If you are a rookie please skip to [this section](#the-best-learning-resources). Important stuff clarified we can proceed with the guide.

## Style guide

It is important to remember why you are writing CoffeeScript in the first place.
Your focus is on readability, better readability than JavaScript while writing less code.
So this guide's job is to put together some tips that will help you achieve that.

### 1. Regarding line writing:
  * Use **2 spaces** to indent, most editors enable you to convert tabs into spaces;
  * The maximum line length is **80 characters**, long lines compromise readability;
  * **Don't** leave **trailing spaces**. Again, you editor can help with that matter;
  * Use **one** blank line to separate function declarations;
  * Use **one** blank line to separate properties within a `Class`;
  * Leave **one** blank line at the **end** of the **code** in each file;
  * **Don't** use blank lines to separate lines within the same function.

### 2. Regarding string usage:
  * Always use double quotes `"` in strings, everywhere;
  * Break long strings, respecting the 80 characters max rule, CoffeeScript supports multi-line strings;
  * Use CoffeeScript's string interpolation instead of concatenation with `+`.

### 3. Regarding comments:
  * Use **single line** `#` comments most of the time;
  * **Only** use multi line comments `###` on the header which contains information about the file.
  * Use **one space** after the single `#` symbol before starting the comment sentence, this improves readability.
  * When using external **automatic documentation** software you may override this rule if necessary.

  Example:

    ```coffeescript

    add = (num1, num2) ->
      return num1 + num2

    result = add(1, 2)

    # Breaking line because string has more than 80 characters
    # Important: Check if your spacing is right before breaking
    string = "We performed a sum between 1 and 2 and the result
     is #{result}"
    ```

### 4. Regarding variable writing:
  * Variables should be written in **lowerCamelCase**;
  * Constants should be written in **UPPERCASE** with `_` if necessary;
  * Class names should be written in **UpperCamelCase**;
  * **Make scope clear**, as CoffeeScript always assume the keyword `var` when a new variable is presented to avoid accidental global scoping you must be sure that your variable is declared in the right spot. Remember that CoffeeScript also always automatically declare your variable before using it if it does not found an existing variable with the same name.
  * You should avoid unnecessary **global variables** but if you want them you should attach your variable to the `window` object in the browser or declare it on the global scope on other JS environments.

Problem:

  ```coffeescript
    # This is a scope problem, the logging of the foo variable
    # will be undefined because CoffeeScript correctly defined it
    do ->
      foo = "bar"

    console.log(foo)
  ```

Solution:

  ```coffeescript
    # To solve the problem we must declare foo
    # foo must assume a default value so CoffeeScript will
    # declare it for us
    foo = ""

    do ->
      foo = "bar"

    # Now it's logging "bar"!
    console.log(foo)
  ```

### 5. Regarding CoffeeScript's special features
  * **Always return** unless it's void, do not use CoffeeScript implicit `return`;
  * When you have to pass a **variable number of arguments** to a function, use **splats**;
  * Instead of executing simple functions in loops use **object or array comprehensions**;
  * **Don't** use **object or array comprehensions** for **complex stuff**, it makes it hard to read;
  * Make use of closures created with ```do``` when building your modules;
  * Use CoffeeScript's boolean flexibility to improve readability when suitable;
  * Use CoffeeScript's existential operator ```?```;
  * **Don't use commas** when writing long literal array and object notations, instead, add line breaks at each node.

## About the usage of parenthesis
  * CoffeeScript gives you the option to omit parenthesis on certain situations, it's OK to do it everywhere you can **but function calls**, you should call functions with **arguments surrounded by brackets**. Always.

Example:

  ```coffeescript
  # Using closure, you can add arguments here as well
  do ->

    # Array declaration without commas
    pilots = [
      "Senna"
      "Alonso"
      "Schumacher"
      "Vettel"
      "Hamilton"
      "Barichello"
    ]

    # Sample podium function, showing how you can use splats,
    # string line breaks, string interpolation and implicit return
    podium = (fisrt, second, third, rest...) ->
      "Gold Trophy: #{first}, Silver trophy: #{silver}, Bronze trophy:
       #{bronze}. Contenders: #{rest.join(",")}"

    # Calling a function with splats
    podium pilots...

    # A more friendly approach to boolean values.
    # No need to use splats here, I just use to reuse the elements
    # I already had.
    didSennaWin = (first, pilots...) ->
      if first is "Senna"
        return yes
      else
        return no
  ```

### 6. Simplify complex code with classes and modules
  * Use CoffeeScript classes when applicable
  * Classes create closures
  * Classes are inheritable
  * Classes are reusable

Example:

  ```coffeescript
  ###
    Example class Car
    Author: Matheus R. Kautzmann
  ###

  class Car

    # Instance properties

    # Default brand
    brand: "Other"

    # Car start at distance 0
    distance: 0

    # Default year
    year: 2013

    # Air Conditioner is off by default
    airConditioner: off

    # Color is white by default
    color: "White"

    # Class properties

    @possibleBrands: [
      "Audi"
      "Mercedes"
      "BMW"
      "Ferrari"
      "Lamborghini"
      "Volvo"
      "Fiat"
      "GMC"
      "Toyota"
      "Nissan"
      "Renault"
      "Other"
    ]

    # Class methods

    @currentModelYear: ->
      actualDate = new Date()
      actualYear = actualDate.getFullYear()
      # Explicit return statement improves readability
      return (actualYear + 1)

    # Constructor
    constructor: (brand, model, year, color) ->
      @brand = brand if brand in Car.possibleBrands
      @model = model
      @paint(color)
      @year = year if year <= Car.currentModelYear()

    # Instance methods

    move: (distance) ->
      if distance? then @distance += distance

    paint: (color) ->
      @color = color if color?

    toggleAirConditioner: ->
      if @airConditioner
        @airConditioner = off
      else
        @airConditioner = on

  ```

### 7. Regarding usage of generators

  * Since version 1.9.0 CoffeeScript supports ES6 generators;
  * Use generators to create custom functions that yields series of values;
  * Remember that CoffeeScript is just JS, so your target platform must support ES6 generators feature;
  * Use it when it makes sense, like when you are writing a function that you would later call iterating over a specific series of values.


Example:

  ```coffeescript
    # Creating factorial generator to later iterate on
    factorial = ->
      num = 0
      result = 0
      loop
        result = num * result
        if num < 2 then result = 1
        if num is 2 then result = 2
        num++
        yield result
      return

    # Iterating over factorial generator
    it = new factorial()
    # Get factorials from 0 to 10
    console.log(it.next()) for i in [0..10]
  ```

## Debugging

Sometimes it's hard to follow the changes in code between CoffeeScript and compiled JS. To help address this issue Source Maps were introduced in CoffeeScript in version 1.8.0.

Source Maps tells browsers that the JS file was generated by CoffeeScript, so the browser can map JS runtime to the original file written in CoffeeScript allow debugging directly with the CoffeeScript file! This helps a lot when checking your code for bugs because you just need to check your .coffee files.

To use source maps you must enable the feature in your CoffeeScript compiler, the CoffeeScript module for Node.JS has the option available as an argument, you can call the command in your CLI as shown below.

`coffee --compile --map myfile.coffee`

## Development process

### 1. Code quality
  * Always lint your CoffeeScript code, you can use [CoffeeLint](http://www.coffeelint.org/);
  * Do not lint the JS generated by CoffeeScript. Instead, lint your CoffeeScript directly as said above;

### 2. Write tests
  * You should write automated tests for your CoffeeScript app;
  * Write your tests in CoffeeScript, [Mocha](http://mochajs.org/) is a good option;
  * If you need a browser environment, [PhantomJS with Mocha](https://github.com/metaskills/mocha-phantomjs) is a nice option.

### 3. Compile your CoffeeScript
  * Always compile your CoffeeScript to JS, never use CoffeeScript code directly. Unless your are writing a CoffeeScript web transpiler or something like that;
  * You can use the CoffeeScript node module itself to compile .coffee files.

### 4. Minify your generated JS
  * Use [UgilifyJS](https://github.com/mishoo/UglifyJS) or [YUI Compressor](http://yui.github.io/yuicompressor/) to do this.

### 5. Sketch a good build process
  * Use [Grunt](http://gruntjs.com/) or [Gulp](http://gulpjs.com/) to setup your build process;
  * Do everything important in this process: lint, test, compile to JS, minify JS, etc;
  * It is strongly recommended the use of a continuous integration server, [Travis CI](https://travis-ci.org/) is an excellent option if you use GitHub.


## The best learning resources

Learning more about CoffeeScript is always nice. Here are listed some great resources to get started with CoffeeScript or, if you are already experienced with it, you can learn some good tips and tricks you can use in your code.

### Books and other textual resources

* [CoffeeScript Cookbook](http://coffeescriptcookbook.com/)
* [Smooth CoffeeScript](http://autotelicum.github.com/Smooth-CoffeeScript/interactive/interactive-coffeescript.html)
* [CoffeeScript official website](http://coffeescript.org/)
* [Testing with CoffeeScript](https://efendibooks.com/minibooks/testing-with-coffeescript)

### Screencasts

* [Introduction to CoffeeScript](http://screencasts.org/episodes/introduction-to-coffeescript)
* [Peepcode CoffeeScript screencast](https://peepcode.com/products/coffeescript)

### Slides

* [CoffeeScript - take a sip of code](https://speakerdeck.com/tsironis/coffescript-take-a-sip-of-code)
* [CoffeeScript - Six reasons and a movie](https://speakerdeck.com/tsironis/coffescript-take-a-sip-of-code)

### Virtual courses

* [Codeschool CoffeeScript course](http://www.codeschool.com/courses/coffeescript)
* [Tuts+ CoffeeScript course](https://tutsplus.com/course/cleaner-code-with-coffeescript/)

### Step by step tutorial

* [Carbonfive tutorial](http://coffeescript.carbonfive.com/)

## Author

This guide is being written by [Matheus Kautzmann](https://github.com/mkautzmann/) and it is always changing. This repo is always open to contributors, so if you disagree of something present in this document or want to add an important thing to it feel free to make a pull request or open an issue.

## License

This project is under MIT License.

The MIT License (MIT)
Copyright (c) 2015 Matheus Kautzmann

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
