# Variables Explained in Ruby

The first year of programming in JavaScript and Ruby, I didn't ***actually*** know what variables were nor did I know the best mental model for thinking about variables. 

Looking back, this led to some confusion with bugs that I didn't fully understand. I fixed a lot of these bugs with _hacking and slashing_, but didn't truly understand why these bugs arose.

I'm hoping this article will clear up what variables ***actually*** are in most OOP languages like Ruby, JavaScript, Java, Python, etc...

Are you new to programming, a JavaScript dev or an experienced Rubyist? 

Like I was, you may not be aware of how variables actually work...

Let's get started!

## How You're Originally Taught About Variables

_(In this article we'll use Ruby for our examples because of its easy to read syntax, but this stuff will apply to most other OOP languages as mentioned in the intro.)_

When we first learn about variables we generally learn that variables ***store*** values. 

We go through a tutorial or walkthrough and we create our first variable, _like this_:
```ruby
x = "hello world"

```

Wow, look at that! We've initialized (created) a new variable called `x` that ***stores*** the value of `"hello world"`.

_(Notice the emphasis on **"stores"**...)_

Now when we reference or type the variable's name in our code it will give us the value of `"hello world"`.

```ruby
puts(x)
# Outputs: hello world

```

> `puts` is a method in Ruby that will output the returned value to the console. If you're familiar with JavaScript, this is basically `console.log`. 
>
> In this case we'll be outputting: "hello world"

As you can see `x` _appears_ to be "holding" the String object `"hello world"`.

#### Right now variables probably look something like this in your head:

<img alt="Image of a variable being represented as a container" src="/Users/jacksebben/LaunchSchool/RB109/images/variable_as_a_containers.jpg">

Variables look like containers that hold values, and when you reference that varaible you're essentially reaching into the container and grabbing the value that it holds.

This mental model works well for beginners. 

It's simple and easy to conceive which really allows them to hit the ground running. 

The problem with this approach on this mental model is that it is not quite accurate nor is it the ideal way to think about variables. 

This initial mental model will eventually ause confusion when you go about passing variables around in your application.

Knowing how data flows in a program is **everything**.

## What a Variable Actually is?

_What happens when you initialize a variable?_

_Where is that newly made value held?_

_What does the variable actually represent?_

Great questions _(says the guy who typed the questions)_!

Objects are stored in a slot of memory in your program.

> Note: if you don't know exactly what objects are, just think of them as 'values' or pieces of 'data' for now

And ***variables*** are just a way for you to reference those values from thos slots of memory.

If we have an object stored in memory, we need a way to reference that space in memory in order to find it and use it.

Otherwise, how else are we going to get that object and use it in our program?

The more accurate definition for variables:

_"Variables are **references** to objects in memory."_ 

Everytime you intialize a variable you are creating a reference or pointer, that points to a slot in memory that holds an object:
```ruby
x = 'hello world' 
# `x` points to a slot in memory with the String object: 'hello world'

nums = [1, 2, 10]
# `nums` points to a slot in memory with the Array object: [1, 2, 10]

floats = 10.4
# `floats` points to a slot in memory with the Float object: 10.4

```

#### Here's the updated and more accurate mental model for variables:

<img alt="Image of variables being represented as references" src="/Users/jacksebben/LaunchSchool/RB109/images/variables_as_references.jpg">

As you can see, variables are just "pointers". They "point to" places in memory (the boxes in the image that hold objects).

To explore this concept more deeply, let's look _at this:_
```ruby
a = 101

b = a

c = b

```
If we were to output `a`, `b` and `c`, what do you think we would get?
```ruby
puts a # 101

puts b # 101

puts c # 101

```
For all 3 variables we would get an output of `101` to the terminal.

***What's happening here?***

Let's break it down, line-by-line:
1. We intialized variable `a` to point to the location in memory that holds the Integer object, `101`.
2. We intialized variable `b` to the same value as `a`, so it points to the same memory location as `a`, which holds the Integer object, `101`.
3. We intialized variable `c` to the same value as `b`, so it points to the same memory location as `b`, which holds the Integer object, `101`.

It's variables using other variables to figure out where they should reference/point to in memory.

<img alt="Image of variables being represented as references" src="/Users/jacksebben/LaunchSchool/RB109/images/variables_referencing_varaibles.jpg">

***It's super important to note:*** The variables are all separate pointers/references. They don't share reference to `101`. 

---

"So how does this help me??"

Understanding this concept doesn't change much in terms of initializing variables or referencing variables to access objects. But, what it does change is how you go about passing variables to methods/functions and how you mutate/change the value of objects.

This is where the biggest bugs and errors are made! 

I will cover this more in depth in my upcoming articles: _Mutating VS Non-mutating in Ruby_ and _Passing Objects to Methods in Ruby_

If you enjoyed this article please make sure to applaud!
Any feedback, good or bad is very much appreciated.

Thank you ✌️