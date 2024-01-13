# Launch School's Live Sessions: Part 2
> [Launch School Live Session: Beginning Ruby Part 2](https://launchschool.medium.com/live-session-beginning-ruby-part-2-f87d821ce926)

<br>

## Local Method Scope 🔎
#### Couple Rules for Method Scope:
1. Variables initialized in a method scope **_are not_** accessible to the outer scope.</br>
_Example:_
```ruby
def method_1
  a = 10
end 

puts a # This will produce an error
```
If we wanted to be able to access `a` initialized in `method_1` we would have to return it.</br>
_Like so:_
```ruby
def method_1
  a = 10 

  # Some code here...

  return a 
end 

puts method_1 # This will output: 10

a = method_1  # We can also initialize an `a` variable and assign it to what the method return
puts a        # This will output: 10
```
<br>

2. Methods **_do not_** have access to variables in the outer scope unless passed as arguments to the method.
_Example:_
```ruby
a = 10

def method_1
  puts a
end 

method_1 # Returns an error because `a` in the outer scope can't be accessed from inside `method_1`
```
If we wanted to give access to `a` in `method_1` we would have to explicitly pass `a` to it.</br>
_Like so:_
```ruby
a = 10

def method_1(param)
  puts param
end 

method_1(a) # This will output: 10
```
<br>

## Mutating 🆚 Non-Mutating
#### Definitions:
1. _Mutating_
  Mutating means the method will directly reference and modify the calling object.

2. _Non-mutating_
  Non-Mutating means the methods will either:
  - Creates and returns a new object with a new space in memory </br>
  (This will happen if the result of the method returns a mutable object or if the method is acting upon an immutable calling object)
  - Returns an existing object in memory </br>
  (This will happen if the result of the method is an immutable object)
<br>

_Non-mutating example:_
```ruby
str = "hello"

def method(param)
  param + " world" # Addition is non-mutating, it creates and returns a new object in memory
end 

puts method(str) #=> hello world
puts str #=> hello
```
> The above example is non-mutating. `+` does not mutate the caller object. </br>
> Remember, `param + " world"` is the same as saying: `param.+(" world")`
<br>

_Mutating example:_
```ruby
str = "hello"

def method(param)
  param << " world" # `<<` is mutating, it directly modifies the caller object
end 

puts method(str) #=> hello world
puts str #=> hello world
```
> The above example is mutating. `<<` does mutate the caller object. </br>
> Remember, `param << " world"` is the same as saying: `param.<<(" world")`
<br>

## Side Effect or Return: Choose One
#### Definitions:
1. _Side Effect_
> A side effect is a change that's been made to your code outside of the method scope you're in.
> Examples of side effects include: Mutating an object, changing data in your program, and changing the display of the terminal
> This does **NOT** include returning a new object.

2. _Meaningful Return Values_
> When a method returns a new object that you use with reason and intent. This is **NOT** mutating a caller object or an argument.

<br>

Methods you create should either produce a/some side-effect(s) or return a meaningful value. Methods should avoid doing both. 
<br>

_Why should we avoid doing both?_
> Because we want to separate concerns. Making sure our method is doing one thing will help us predict what a method will do and what it's intention is. When we get our methods to do multiple different things in different areas we often times are making our app more dependent on that method. If the method breaks there's a good chance that many of the operations crammed in it will break too. Not to mention methods are generally easier for us to understand if we keep them short and concise in their operations.


