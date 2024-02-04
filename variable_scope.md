[[Variables#_ Variable Scope _ |As simply defined here]]... Is used to describe where a #variable can and cannot be accessed from within a program. A variable's scope is determined by where a variable is initialized within the program and where in the program it is attempting to be accessed from.

A #variables_scope is determined by method definitions or #blocks. 

---

## Variables and Method Scopes

#### Variable Scope For Methods

Variables defined within [[Methods#_Method Definition_|method definitions]] are ***scoped*** to that method's definition. This means variables initialized between the `def` and `end` keywords of a method definition, won't be accessible to the codebase outside of that method definition.

**Example**
```ruby
def method_name
	x = 10
end 

puts x # will throw an error. `x` was initialized within `method_name`'s definition, meaning we can't access it from outside of that definition
``` 

As seen in the above example, when an attempt to access/reference the `x` variable initialized within the method definition, an error is thrown.

Variables initialized within a method definition can only be directly reference and accessed from within that method definition.

**Example:**
```ruby
def method_name
	x = 10
	puts x
end 

method_name() # the method successfully executes and outputs `10` to the terminal via the `puts` method
```
As seen above, the initialized `x` variable was successful accessed and referenced form within the method's definition.

#### [[Methods#_ Variable Scope Variable and Method Scopes Method Scope _|Method Scope]]

Method scope, it defines what the method can access and reference. Method's have a self-contained scope, meaning they only have access to variables initialized within their definitions. 
Method's cannot access variables initialized in the outer scope.

**Example:**
```ruby
x = "hey"

def print_thing
	puts x
end 

print_thing() # throws an error because the outer scoped `x` variable can't be accessed from within the method's definition
```
As observed, the method in the example above, upon execution, cannot access the `x` variable that it is referencing on the first line. The `x` variable referencing `"hey"` is out of that method's scope.

Methods are like ***self-contained bubbles***. The method only knows what's going on in it's own world (in its definition) it can't directly access variables from outside of it's world. Nor can variables from within the method be accessed from outside of its world.

**Example:**
```ruby
x = "hello"

def print_things
	x = "howdy"
	puts x
end

puts x         # outputs: hello
print_things() # outputs: howdy
```
This is a good example showcasing scoping of variables when it comes to methods.
Inside the method definition, the method only sees the `x` variable initialized within it's scope, therefore when we invoke the `print_things` method and it invokes `puts x` within its definition, `howdy` is outputted to the terminal. When `puts x` is invoked in the outer scope, on the second last line Ruby only _sees_ the `x` variable that was initialized on the first line in the outer scope, which is why `hello` is outputted to the terminal.

#### Summarizing Method Scope
- Variables initialized within method definitions can only be directly access and modified within that method's definition

- Variables in the outer scope can't be directly accessed from within a method definition

- Methods can be thought of as **self-contained bubbles** - It can't see outside of its _"method bubble"_ and nothing can see into it.
---

## Variables and Block Scopes