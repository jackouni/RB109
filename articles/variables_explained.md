# Variables Explained in Ruby

The first year of programming in JavaScript and Ruby, I didn't ***actually*** know what variables were nor did I know the best mental model for thinking about variables. 

Looking back, this lead to some confusion with bugs that I didn't fully understand. I fixed a lot of these bugs with _hacking and slashing_, but didn't truly understand why these bugs arose.

I'm hoping this article will clear up what variables ***actually*** are in most OOP languages like Ruby, JavaScript, Java, Python, etc...

Are you new to programming, a JavaScript dev or an experienced Rubyist? 

Like I was, you may not be aware of how variables actually work...

Let's get started!

## How You're Originally Taught About Variables

_(In this article we'll use Ruby for our examples because of its easy to read syntax, but this stuff will apply to most other OOP languages as mentioned in the intro.)_

When we first learn about variables we generally learn that variables ***store*** values. 

We get a run through of a tutorial or walkthrouh and we create our first variable, _like this_:
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

Right now variables probably look something like this in your head:

<img alt="Image of a variable being represented as a container" src="/Users/jacksebben/LaunchSchool/RB109/images/variables_as_containers.jpg">

Variables look like containers that hold values, and when you reference that varaible you're essentially reaching into the container and grabbing the value that it holds.

This mental model works well for beginners. 

It's simple and easy to concieve which really allows them to hit the ground running. 

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