# <ins>RB101/RB109 MEGA-LIST</ins>
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
    - #### Logical & Comparison Operators 🧠
      - Short Circuiting ⚡️

3. ### Pre-Coding Processes 🛠️
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

---------------------------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------------------------

<br>

# Truthy & Falsy Values ☯️
### Defining Terms 📖
***Expression :*** 
  > An expression is any piece of code that can be evaluated down to a single return value. This includes almost everything in Ruby </br>
  > Conditionals, objects, logical expressions, variables, methods, loops, arithmetic operations and etc </br>
  > Are all things that could techincally be considered expressions. </br>
  > In some programming languages there are constructs that don't allow things like loops and conditionals to return a value. In Ruby almost everything returns a value, therefore almost everything in Ruby can be considered an expression.

***Boolean Expression :***
  > This is an _expression_ that evaluates and returns either a `true` or `false` value.

***`true` :*** </br>
  > `true` is an object in Ruby that represents the boolean 'true'. </br>
  > The `true` object is often times returned from conditional statements, comparison expressions or logical expressions to express the 'true' or 'truthy' value of an expression. </br>
  > Every expression in Ruby will evaluate to `true` except for values of `nil` or `false`

***`false` :*** 
  > `false` is an object in Ruby that represents the boolean 'false'. </br>
  > The `false` object is often times returned from conditional statements, comparison expressions or logical expressions to express the 'false' or 'falsy' value of an expression. </br>
  > The only objects and return values that will evaluate to `false` are `false` itself and `nil`. 

***Operator :***
  > A symbol used in an expression that performs an operation on one or more values. These values are genreally known as _operands_.
  > _Example:_ `a && (b * 10)` </br>
  > Where `a` and `(b * 10)` are operands to the operator, `&&`. </br>
  > And `b` and `10` are operands to the operator, `*`.

***Operand :***
  > A value being operated on by an operator. </br>
  > _Example:_ `(a + b) > 100` </br>
  > Where `(a + b)` and `100` are operands to the operator `>`.
  > And `a` and `b` are operands to the operator, `+`.

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

---------------------------------------------------------------------------------------------------------

<br>

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

---------------------------------------------------------------------------------------------------------

<br>

### Logical & Comparison Operators 🧠
  Logical and comparison operators are super important in control flow and conditional statements in programming in Ruby (and in general). </br>
  Comparison operators are used to compare two operands against eachother and return a boolean based on that comparison. </br>
  Logical operators are used to combine multiple expressions and determine how the expressions are evaluated, resulting in a boolean. These are used in more complex conditional statements.</br>
  > _Comparison operators include:_
  > - `==` ~ Equality operator
  >   - Is a binary operator (takes 2 operands) 
  >   - If both operands are equal in value, `true` is returned, otherwise, `false` is returned
  > - `<=` ~ Equal to or Less than
  >   - Is a binary operator (takes 2 operands)
  >   - If the left operand is equal to OR less than the right operand, `true` is returned, otherwise, `false` is returned
  > - `>=` ~ Equal to or greater than
  >   - Is a binary operator (takes 2 operands)
  >   - If the left operand is equal to OR greater than the right operand, `true` is returned, otherwise, `false` is returned
  > - `>` ~ Greater than
  >   - Is a binary operator (takes 2 operands)
  >   - If the left operand is greater than the right operand, `true` is returned, otherwise, `false` is returned
  > - `<` ~ Less than
  >   - Is a binary operator (takes 2 operands)
  >   - If the left operand is less than the right operand, `true` is returned, otherwise, `false` is returned
  > - `!=` ~ Inequality operator
  >   - Is a binary operator (takes 2 operands)
  >   - If both operands are ***NOT*** equal in value, `true` is returned, otherwise, `false` is returned
  > <br>
  >
  > _Logical Operators include:_
  > - `&&` ~ AND
  >   - Is a binary operator (takes 2 operands)
  >   - If both operands have to evaluate to `true` in order for the expression to return `true`  
  >   - Evaluates from left operand to right operand
  > - `||` ~ OR
  >   - Is a binary operator (takes 2 operands)
  >   - If one of the two operands evaluates to `true` the expression will return `true`
  >   - Evaluates from left operand to right operand
  > - `!` ~ NOT
  >   - Unary operator (takes 1 operand)
  >   - Negates the truthy/falsy value of the operand </br>
  >
  > <br>
  > 
  > #### **Short Circuiting** ⚡️
  > As mentioned above, binary logical operators like `&&` and `||` will evaluate objects from left to right. </br>
  > The concept of ***short circuiting*** is when our expression with a logical operator doesn't evaluate the right operand in the expression. </br>
  > 
  > _How does this work and why?_ </br>
  > <br>
  > In the case of the `&&` operator, both operands, left and right, have to evaluate to `true`. </br>
  > This means if the first operand, the left one, evaluates to `false`, then there is no point in evaluating the right operand as both operands have to evaluate to `true` anyways, so the overall expression cannot be `true`. </br>
  > So the `&&` stops it's evaluating if it encounters an operand that returns `false`, meaning if the left operand evaluates to false, then the right operand is never evaluated. </br>
  > <br>
  > In the case of the `||` operator, only 1 operand has to evaluate to true in order for `true` to be returned from the  logical expression. </br>
  > This means, if the first operand evaluates to `true`, then the expression stops evaluating and returns `true`, never evaluating the second operand. And why would it? If it only needs one of the operands to evaluate to `true` then it doesn't need to evaluate the next operand. </br>
  > <br>
  > Short circuiting is when an expression using a logical operator returns a value before evaluating the entire expression.
  > <br>
  > _Here's an example to illustrate:_
  > ```ruby
  > a = nil && 10
  > b = 10 || false
  >
  > p a # nil
  > p b # 10
  > ```
  > In the example above, `a` evaluates to `nil` because `nil` was the last operand to be evaluated in the expression. </br>
  > `b` evaluates to `10` because `10` was the last operand to be evaluated in the expression.

<br>

---------------------------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------------------------

<br>

# Pre-Coding Processes 🛠️
### Defining Terms 📖
***Pseudocode :*** 
  > Code that mimics spoken language, like English. This code is not machine-readable or used in production but is used for abstracting out the syntax of a problem or application in a way that is easier to conceptualize.

***Flowchart :*** 
  > A visual illustration that helps map out the flow of an application using geometric shapes and lines.


  

<br>


