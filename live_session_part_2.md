# Launch School's Live Sessions: Part 2
> [Launch School Live Session: Beginning Ruby](https://launchschool.medium.com/live-session-beginning-ruby-part-2-f87d821ce926)

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
  1. Creates and returns a new object with a new space in memory </br>
  (This will happen if the result of the method returns a mutable object or if the method is acting upon an immutable calling object)
  2. Returns an existing object in memory </br>
  (This will happen if the result of the method is an immutable object)
<br>

#### Why does it work like this though?


