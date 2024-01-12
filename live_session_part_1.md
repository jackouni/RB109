# Launch School's Live Sessions: Part 1
> [Launch School Live Session: Beginning Ruby](https://launchschool.medium.com/launch-school-live-session-beginning-ruby-c6432494ab34)

<br>

## Syntactic Sugar 🍭

Ruby uses a lot of syntactical sugar to make it's syntax appear more elegant and English-like.
This comes at some pros and cons though:
#### Pros:
- It's very easy to read
- It's more flexible
- Allows for more brevity and conciseness with our code
#### Cons:
- Being flexible means it can be prone to certain errors, because of the lack of straight-forward rules and syntax.
- Can cause confusion with variable and method naming. (Are we invoking a method or a variable? Idk?)

<br>

Methods in Ruby don't require parenthesis for invocation, in fact, they are optional.</br>

There are many details in Ruby that are hidden from us to make the code read easier for humans. 
Here's an example of how Ruby can make operators look like methods:
```ruby
a = "Howdy"
b = " Partner"

a << b
```
The above code is the same as this:
```ruby
a = "Howdy"
b = " Partner"

a.<<(b)
```
> The `<<` operator is just a method. 
> Because it doesn't require dot notation or parenthesis to be invoked on the `a` object, it disguises itself as a regular operator.
<br>

Even reassignment is like this:
```ruby
arr = [1, 2, 3]

arr[2] = 40
```
The above code is the same as this:
```ruby
arr = [1, 2, 3]

arr.[]=(2, 5)
```
> This means `[]=` is a method even (a setter method to be more specific). 
> But with some syntactic sugar it looks like pure reassignment. 
<br>

## Keeping this in mind:

> Ruby abstracts a lot of details out of the code. With syntactical sugar we get a lot of lovely looking and elegant code.
> But, remember this while reading and writing Ruby code, remember that a lot of these operations you're performing may be methods in disguise.
<br>

## Where Does Code Come From:
###### Code in our Ruby apps can come from a few places:
1. #### The Core Library
  - The built-in library of methods and modules in Ruby
  - The fundamental building block methods and modules of Ruby
  - Are built-in and ready to go - no need to download or use `require` keyword to use.
2. #### The Standard Library
  - These are extra methods, and modules that come with Ruby but are not pre-loaded like the Core Library. This is done to save space.
  - These are extra features that you might want to take advantage of but aren't as essential as the Core Library API.
  - Must use the `require` keyword and a string reference to the methods and/or modules you want to use.
3. #### Ruby Gems
  - These are 3rd party libraries that you can download and use in your application from other developers and entities.
  - Generally, Rubyist use a lot of different gems in their applications.
  - Must first download using `gem install` command and then use `require` keyword with string reference to the modules/methods you want to use.
<br>




