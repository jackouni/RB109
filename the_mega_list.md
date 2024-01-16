bbbbbbbbbbbb# RB101/RB109 MEGA-LIST
> This is a file where I will be collecting as many lessons and important material from RB101. </br>
>
> **My goal with this document:**
> 1. Provide concise and exact definitions for common terms. </br> 
>     _(Refer to "Defining Terms" sections)_
> 2. Provide walkthroughs of the material
> 3. Provide practice questions with answers (that you can toggle to show/hide) from both the course material and my own creation.

<br>

## Table Of Contents:

1. ### Ruby Style 🎨

2. ### Truthy & Falsy Values ☯️
    - #### Defining Terms 📖
    - #### `true` & `false` 🆚 Truthy & Falsy  
    - #### Logical & Comparison Operators
      - Short Circuiting

3. ### Pre-Coding Processes
    - #### Defining Terms 📖  
    - #### Pseudocode
    - #### Flowcharts

4. ### Ruby Version Managers

5. ### Rubocop
    - #### Defining Terms 📖
    - #### What is Rubocop?

6. ### Debugging

7. ### Operator Precedence
    - #### Defining Terms 📖

8. ### Variables
    - Variables as pointers
    - Variable shadowing
    - Local variable scope in relation to method definitions
    - Local variable scope in relation to blocks, including nested blocks and peer blocks
    - Scope of constants
    - Mutating values vs. reassigning variables

9. ### Methods:
    - Method definition vs. method invocation
    - Passing and using blocks with methods
    - Parameters vs. arguments
    - Default parameters
    - Implicit vs. explicit return values
    - Mutating vs. non-mutating methods
    - Using method return values as arguments to other methods

10. ### Mutable vs. immutable data types
11. ### Output vs. return
12. ### How Objects Are Passed Around
      - Pass By Reference
      - Pass By Value
      - Call By Sharing

<br>
<br>
<br>

---------------------------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------
<br>

# Ruby Style 🎨
In Ruby there are styling conventions that are followed to maintain better readability and consistency across developer's appilications. Here are some of the general style rules for Ruby that most developers follow:
- For blocks, if the code can be short and concise make it a one-liner using `{ }`. Otherwise use a `do/end`.
- Always use _snake_case_ for nameing variables
- Always use _UPPERCASE_ for naming constants
- Always use _CamelCase_ for naming Classes
- Indentations with tabs is 2 spaces

<br>
<hr>
<hr>

# Truthy & Falsy Values ☯️
### Defining Terms 📖
***`true` :*** </br>
  > `true` is an object in Ruby that represents the boolean 'true'. </br>
  > The `true` object is often times returned to from conditional statements and conditional or logical expressions to express the 'true' or 'truthy' value of an expression. </br>
  > Every expression in Ruby will evaluate to `true` except for values of `nil` or `false`

***`false` :*** 
  > `false` is an object in Ruby that represents the boolean 'false'. </br>
  > The `false` object is often times returned to from conditional statements and conditional or logical expressions to express the 'false' or 'falsy' value of an expression. </br>
  > The only objects and return values that will evaluate to `false` are `false` itself and `nil`. 

***Expression :*** 
  > An expression is any piece of code that can be evaluated down to a single return value. This includes almost everything in Ruby </br>
  > Conditionals, objects, logical expressions, variables, methods, loops, arithmetic operations and etc </br>
  > Are all things that could techincally be considered expressions. </br>
  > In some programming languages there are constructs that don't allow things like loops and conditionals to return a value. In Ruby almost everything returns a value, therefore almost everything in Ruby can be considered an expression.

***Boolean Expression :***
  > This is an _expression_ that evaluates and returns either a `true` or `false` value.

***Truthy :***
  > '_Truthy_' is a term used to describe any value that evaluates to `true` in a boolean context. </br>
  Luckily, Ruby follows 1 simple rule: Every value can be evaluated as `true` (truthy) except for `false` and `nil` (falsy).<br>
  Because of this, it allows us to compare values of varying data types to return a value from a boolean expression.</br>
  It allows us the ability to make expressions _like this:_ </br>
  > ```ruby
  > a = 'hello' || nil # 'hello' will evaluate to `true`. 'hello' is 'truthy'.
  >
  > puts a # "hello"
  > ```
  > There are many more examples, but this is just one to illustrate the idea of truthy.

***Falsy :***
  > 'Falsy' is a term used to describe any value that evaluates to `false` in a boolean context. </br>
  > `nil` and `false` are the only 'falsy' values in Ruby. </br>
  > As with 'truthy', 'falsy' is a way to allow us to compare values of varying data types to return a value from a boolean expresion.

<br>
<hr>

### `true` & `false` 🆚 Truthy & Falsy 
  `true` and `false` are not strictly equivalent to other values that are 'truthy' or 'falsy'. </br>
  To illustrate, here is an example:
  > ```ruby
  > 'hello' == true # false
  > ```
  > This is because the truthy value of 'hello' is just a mechanism for a String to return a `true` value in a boolean context. </br>
  In context to our example, we are comparing the the String object 'hello' as whole, to the `true` object as a whole. </br>
  Truthy and falsy are simply just ways to describe if something is 'true' or 'false', it does not make the objects themselves `true` or `false` objects. </br>
  In the context of representing an instance of a `true` or `false` object, truthy and falsy values are not this.
  This concept is the same for falsy values as well:
  > ```ruby
  > nil == false # false
  > ```

<br>
<hr>

### Logical & Comparison Operators
