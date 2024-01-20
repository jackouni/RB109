# Precedence In Ruby - Is Not So Simple

After 1.5 years of coding and building a couple calculator apps, an etch-a-sketch app, command line programs, rock paper scissors, studying my head off and creating some other small applications; all from scratch. I only just found out the full depth of the concept of Precedence. </br>
<br>
You'll often hear:</br>
_"Precendence is the order in which expressions get evaluated."_ </br>

<br>
While this is sort of true, it gets more complicated than that. </br>
Even some seasoned Ruby devs who have built decent sized programs still don't fully understand Precedence... </br>
<br>
Let's with a quick review of the basics and slowly ramp up to some more tricky concepts and nuances. And yes, I know what a lot of you Rubyists and devs are thinking: "Okay, I'll just skip this part because I totally understand the basics" - hold your horses partner! </br>
I recommend reading through this and reviewing this for a couple reasons: </br>
- Help solidifying and re-validate the fundamentals you've already learned
- Reading this will give you a more full context to the nuances I'm about to explain 
<br>

## A Quick Primer
Often times we are taught this concept of Precedence using a similar statement to the one in the beginning of this article:
> _"Precendence is the order in which expressions get evaluated."_ </br>
<br>

Let's expand on that... </br>
_Take this example:_
```ruby
5 + 2 * 10 #=> 25
```
Why is it that we get `25` and not `70`? I mean, in this expression we could start by adding `5 + 2` which is `7` and then doing `* 10` to get `70`. What rules are there that state we first have to do `2 * 10` and then do `5 + 20`? Why? </br>
<br>
To get clear on things, let's first define some basic terms: </br> 
<br>

***Expression***
> "Is any code that can be evaluated down to a single value."

***Evaluate***
> "To return a value from an expression."

***Operand*** 
> "A value in an _expression_ that will be used in an operation, determined by an _operator_" </br>
> For the expression `a + b`, `a` and `b` are the operands to the operator `+`.

***Operator***
> "A symbol or syntax that uses 1 or more _operands_ and performs an operation on them to return a final value." </br>
> For the expression `a + b`, the `+` is the operator that will perform addition on the operands `a` and `b`.

And if you're ever unclear or confused while, refer back to the definitions above.
<br>
<br>

**Almost everything in Ruby can be considered an _expression_.** </br> 
<br>

This is because almost everything in Ruby returns a value... </br> 
A method call returns a value, referencing array indexes will return a value and even variables will return a value... </br>
<br>

Within expressions we can have other nested-expressions. </br> 
In other words, we can have a large expression, but within that large expression we can have multiple other expressions that return values and are then operands to other adjacent operators. Expressions can be as simple as a single variable like `a` (because it's a variable and will return a value) or as complex as `(true && false) || 10 || nil && (100 * 47) || (10 + 2 / 12)` (a little crazy, but you get the point). </br>
<br>

This also means that operands can be expressions themselves. For example, within the expression `(1 + 2) * (3 - 1)`, the nested-expressions `(1 + 2)` and `(3 - 1)` are operands to the operator `*`. When evaluated they return values, but are also being operated on by the operator `*`, that will then return another value. </br>
Overall, the expression `(1 + 2) * (3 - 1)` will be evaluated to `6`. </br>
<br>

Generally, most operators must take 2 operands (binary operators). </br>
But, there are operators that take only 1 operand (unary operators). </br>
There's even one operator that takes 3 (known as the ternary operator). </br>
<br>

Examples:
```ruby
  10 / 2               # Binary: `10` and `2` are operands
  !true                # Unary : `true` is the operand
  value ? true : false # Ternary:`value`, `true` and `false` are operands 
```
<br>

---

## What You're First Taught with Operator Precedence 
_Operator Precedence_:
> "Operator Precedence is a set of rules that determine what operands an operator uses first." 
<br>

Here's an example to illustrate: 
```ruby
1 + 2 * 5 # => 11
```
With 2 binary operators, each needing to take 2 operands, how come we only have 3 operands to go around? </br>
How is the `+` operator going to share `2` with the `*` operator?? </br>
<br>

Using operator Precedence, Ruby can decide which operators operate with first. In the case of the example above, Ruby would do `2 * 5` first, this is because `*` holds higher _Precedence_ than `+`. </br>
If we could go step-by-step through the evaluation of the expression, after the first operation we now have this: 
```ruby
1 + 10
```
And now `+` operates on `1` and `7` to return `11`. </br>
<br>

Let's say we wanted to prioritize `1 + 2` and make Ruby evaluate this part first? Well, we can make it do that by adding brackets around expressions, as bracketed expressions hold nearly the highest Precedence. 
```ruby
# Starting Expression:
(1 + 2) * 5 
```
```ruby
# Next Operation:
3 * 5 # => 15
```
<br>

To really knock this one out of the park let's explore one more example and step through each operation, step-by-step</br>
Here's our last example:
```ruby
10 && 20 + 5 * 2 || 100
```
**1st operation:**
```ruby
# `*` holds highest Precedence, `5 * 2` is operated on first
# `10` is returned from `5 * 2`
10 && 20 + 10 || 100
```
**2nd operation:**
```ruby
# `+` holds next highest Precedence, `20 + 10` is operated on next
# `30` is returned from `20 + 10`
10 && 30 || 100
```
**3rd operation:**
```ruby
# `&&` holds next highest Precedence, `10 && 30` is operated on next
# `30` is returned from `10 && 30`
30 || 100
```
**Last operation:**
```ruby
# `||` holds next highest Precedence, `30 || 100` is operated on next
# `30` is returned from `30 || 100`
30
``` 
<br>

## It's Not Just Precedence, But Also _Order Of Evaluation_
_"Order of evaluation"_ ahaa, this might sound different... (at least for me it did) </br>
<br>

Let's consider:
```ruby
def letter_count(str)
  puts str.size
  return str.size
end  

puts letter_count('a') + letter_count('heyo') / letter_count('hi')
```
Now what do you think this code will output? </br>
Take a guess. </br>
<br>
If you guessed:
```
1
4
2
3
```
You're correct! </br>
<br>

Why didn't our program evaluate the `/` first? I mean, it holds the highest precdence... right? </br>
It looks like Ruby just evaluated our final line of code from left to right. </br>
<br>

Yes `/` holds highest operator precdence in this example, but these operators on the final line need values to operate on. </br> 
Method invocations are not values. So we first have to evaluate them. Ruby tries to evaluate an expression and suss-out any undetermined values from left to right before looking at the operators. </br>
<br>

In this case it runs each method 1 after the other, resulting in the first 3 values being outputted in our terminal.</br> 
The values returned from the methods are the operands that can now be operated on by the operators. </br>
<br>


So, for our example's final expression, we evaluated from left to right invoking methods and then we went by operator precdedence to get values from the operators and their operands. </br>
<br>

_In Ruby, method calls are evaluated before operator precedence is applied._
<br>

Let's look at these:
```ruby
a = b = c = 10
a = 20 + 5 if a == b if b == c
```
`a`, `b` and `c` equal `10`. then we're saying, assign `a` to `20 + 5` (`25`), `if` `a` is the same value as `b` and `if` `b` is the same value as `c`.
<br>

These two lines of code are examples of evaluation happening from right to left.</br> 
Assignment operators and modifiers like `if`, `elsif` and `unless` - evaluate expressions to the right of them first.
<br>

_This is horrible code by the way. And I pray you never see this in the wild (which you most likely won't, so that's good)._
<br>

### Expressions That Never Evaluate...

Sometimes code can be left out of the entire evaluation process due to a concept called ***short circuiting***. </br>
This is happens with the ternary operator, `&&` operator and `||` operator. </br>
_If we look at this code..._
```ruby
100 || ay # 100

nil && ay # nil

false ? ay : "Hi" # "Hi"
```
Notice that we have an uninitialized variable `ay` in our expressions above. Despite this, we never encounter an error. Why is this? </br>
<br>

This is because the expressions stopped evaluating before it could evaluate `ay`. </br>
In the first expression, `100 || ay`, in order for the `||` operator to return a value only one of the operands has to be truthy. In this case it evaluates from left to right and finds that `100` is truthy, so it returns `100`. Why would it even need to evaluate the other operand, the condition has already been met. So, the `ay` operand is never evaluated. </br>
<br>

In the second expression, `nil && ay`, in order for the `&&` operator to return a value it only needs one of the operands to be falsy. In this case it evaluates from left to right and finds that `nil` is falsy, so it returns `nil`. Again, the `ay` operand is never evaluated. </br>
<br>

In the last expression, if the expression before the `?` is truthy it will return the value of the expression after the `?` and before the `:`, if the expression before teh `?` is falsy the ternary will return the value of the expression to the right of the `:` . Because the expression in this example is falsy, `ay` is skipped over and never evaluated and the value of `"Hi"` is returned. </br>
<br>

### More Confusion

Now let's think about blocks in Ruby. We can think of blocks like arguments to methods.

Here's one more weird quirk to consider:
```ruby
arr = ['a', 'b', 'c']

p arr.map {|e| e.upcase} # Outputs: ["A", "B", "C"]
                         # => ["A", "B", "C"]

p arr.map do |e|         # Outputs: #<Enumerator: ["a", "b", "c"]:map>
  e.upcase               # => ["A", "B", "C"]
end 

```
Different outputs?! They do the exact same thing though? </br>
Both expressions are calling the `p` method and passing `arr.map <block>` to it as an argument. </br>
<br>

Blocks in general have the lowest precdence in Ruby. It turns out, `{}` has a slightly higher Precedence than `do...end`. This small gap in Precedence allows for Ruby to evaluate each example slightly different. </br>
<br>

In the first example, `{ }` blocks are given a slightly higher Precedence meaning they _"bind"_ more tightly to it's nearest operator which is `arr.map`. This is much like how `/`'s operands would bind more tightly to it then `+` would. </br>
```ruby
10 + 6 / 2
```
`6` and `2` are more bound to `/` because of its Precedence and therefore `6` and ` 2` are more associated with `/` than to `+`</br>
<br>

`do...end` blocks have a weaker binding to their operands and are less associated with them. In our confusing example above, the `arr.map` is less associated to the `do...end` block. </br>
<br>

Whereas, `{ }` blocks are a bit stronger than `do...end`, enough that `arr.map` has a stronger association to the block and when passed to `p` are passed as a whole. </br>
<br>

In our example, `do...end` is less associated to `arr.map` and `arr.map` is more associated to `p`. </br>
<br>

Because of this, `arr.map` is seen as the argument being passed to `p`. Inside `p` `arr.map` is evaluated and returns an enumerator object. Now `p do...end` is left, and because `p` doesn't take a block, this block is essentially ignored, having no effect. </br>
<br>

Whereas, `{ }` is more associated with `arr.map` and `arr.map {...}` is seen as a whole expression being passed to `p`. In `p` `arr.map {...}` is evaluated and returns the resulting object: `["A", "B", "C"]`</br>
<br>

Here's an example to conceptually illustrate:
```ruby
# `do...end`` conceptually:
p(arr.map) {|e| e.upcase}

# `{}`` conceptually:
p(arr.map {|e| e.upcase})
```
Much like with our simple example of `10 + 6 / 2` you could conceptually think of it as `10 + (6 / 2)`.</br>
<br>
<br>

I hope this clears things up and exposed you to the true depth of precdence and order of evaluation in Ruby.