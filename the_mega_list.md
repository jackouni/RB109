bbb# RB101/RB109 MEGA-LIST
> This is a file where I will be collecting as many lessons and important material from RB101. </br>
>
> **My goal with this document:**
> 1. Provide concise and exact definitions for common terms. </br> 
>     _(Refer to "Defining Terms" sections)_
> 2. Provide walkthroughs of the material
> 3. Provide practice questions with answers (that you can toggle to show/hide) from both the course material and my own creation.

<br>

## Table Of Contents:

1. ### Ruby Style

2. ### Truthy & Falsy Values
    - #### Defining Terms
    - #### `true` & `false` V.S. Truthy & Falsy  
    - #### Logical & Comparison Operators
      - Short Circuiting

3. ### Pre-Coding Processes
    - #### Defining Terms  
    - #### Pseudocode
    - #### Flowcharts

4. ### Ruby Version Managers

5. ### Rubocop
    - #### Defining Terms
    - #### What is Rubocop?

6. ### Debugging

7. ### Operator Precedence
    - #### Defining Terms

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

# Ruby Style
In Ruby there are styling conventions that are followed to maintain better readability and consistency across developer's appilications. Here are some of the general style rules for Ruby that most developers follow:
- For blocks, if the code can be short and concise make it a one-liner using `{ }`. Otherwise use a `do/end`.
- Always use _snake_case_ for nameing variables
- Always use _UPPERCASE_ for naming constants
- Always use _CamelCase_ for naming Classes
- Indentations with tabs is 2 spaces