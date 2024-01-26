# Mutating VS Non-Mutating Methods in Ruby - The Confusing Parts

Here's where beginner, intermediate and even experienced devs slip up.

What is, understanding mutation of objects in OOP.

For this article, examples will be written and given in Ruby because of its super readable syntax, but the concepts generally apply to most other OOP languages like JavaScript, Python, Java, Pearl and so on...

So even if you're not learning Ruby, you can join along and get a better understanding for the OOP language you're coding in.

---

# The Mental Model You'll Need To Learn This Concept

In my last article on Variables in Ruby (and OOP in general), I covered what variables ***actually*** are and the best way to think of them. 

I defined variables as:

_"Variables are **references** to objects in memory."_

As a mental model, variables should look like this to you:

<img alt="Image of variables being represented as references" src="/Users/jacksebben/LaunchSchool/RB109/images/variables_as_references.jpg">

They're references that point to a location in memory that contains an object.

---

# Assignment and Reassignment

What happens when we initialize a variable, _like this?_
```ruby
x = "howdy"
```

Some might answer:
_"We're creating a reference that points to a new location in memory with the newly made object, `"howdy"`."_


And, in this example we just gave above, you would be correct.

But what happens when we _do this?_:
```ruby
x = "howdy"
y = "howdy"
```
**Two questions:**
- Is `y` pointing to the same location in memory as `x`?
- Is the object that `y` points to the same object that `x` points to (`"howdy"`)?

Why don't we find out?
```ruby
x = "howdy"
y = "howdy"

x += "!!"

puts y # Outputs: howdy
puts x # Outputs: howdy!!
```
> **For clarity:** 
> In this example, `+=` is used to concatenate the sub-string (`"!!"`) onto the caller variable (`x`).
> `x += "!!"` is the same as saying: `x = x + "!!"`

In the above example you can see that we changed the value of `x` by adding `!!` to the end of it. 

If `x` and `y` both referenced the same location in memory then changes to the value of `x` would've changed the value of `y`, given that we're referencing the same location in memory with the same object.

And we can see in the example above, that `y` is still pointing to the value `"howdy"` while `x` points to the value `"howdy!!"`

We can use the method `object_id` to further confirm this.
> **`object_id` :**
> `object_id` is a method that shows the _"memory address"_ of an object. This method will return to us the address of the location in memory that the caller variable is in.

Let's try out `object_id`!
```ruby
x = "howdy"
y = "howdy"

x.object_id # returns: 60
y.object_id # returns: 80
```
> **To clarify:**
> On my machine these are the "addresses" returned, on your machine they might be different than `60` and `80`.
>
> Regardless, `x` and `y` on your machine should have different return values from eachother when `object_id` is called on them.

As you can see `x` points to a "memory address" of `60` and `y` points to a "memory address" of `80`.

Because these are two separate objects in two separate places in memory, if we change the value of one, it won't reflect in the other.
```ruby
x = "howdy"
y = "howdy"

y = "partner"

puts x # Outputs: howdy
puts y # Outputs: partner
```

#### For the above example, our mental model might look like this:

<img alt="Image of variables being represented as references" src="/Users/jacksebben/LaunchSchool/RB109/images/x_y_different_slots.jpg">

As discussed in the last article (which again, you should read as a refresher), if we assign a variable to another variable, the first variable will just point to whatever location in memory the second variable in the expression in pointing to. In this case we never initialized a new object, we just told a variable to reference the same location in memory as another variable.

Let's assign `y` to `x`, like this:
```ruby
x = "howdy"
y = x

x.object_id # returns: 60
y.object_id # returns: 60
```

#### As you can see above, `x` and `y` have the same Object ID's. This means they both point to the same location in memory, containing the same object.

<img alt="Image of variables being represented as references" src="/Users/jacksebben/LaunchSchool/RB109/images/x_y_same_slot.jpg">

> **Important to note:**
> `x` and `y` are **not** sharing a pointer/reference, they are two separate pointers that point to the same location in memory.

---

# Where The Confusion Begins

Great! I get that. 

But then why does this happen??:
```ruby
x = "howdy"
y = x

y = "sup?"

puts x # Outputs: howdy
puts y # Outputs: sup?
```
If `y` and `x` share the same reference to a location in memory, then why doesn't the reassignment of `y` to `"sup?"` change the value of the object in the location that `x` and `y` both reference to? We're changing the value of the object that we're pointing to in memory, right?
In this case, the reassignment of `y` should've changed the object that `x` and `y` both point to. Why isn't `x` returning `"sup?"`?

This is where the concept of Mutating VS Non-Mutating methods is introduced.

But first, let's see what happened to the object IDs in our last example:
```ruby
x = "howdy"
y = x

x.object_id # Returns: 60
y.object_id # Returns: 60

y = "sup?"

x.object_id # Returns: 60
y.object_id # Returns: 80
```

We can see that originally in the first 2 lines that `x` and `y` both reference the same location in memory (this is what `object_id` on my machine is calling `60`).

But on our reassignment of `y` to `"sup?"`, `y` now references a different location in memory. Our reassignment has created a new object in a new location.

#### Using our mental model, you can think of it like this:

<img alt="Image of variables being represented as references" src="/Users/jacksebben/LaunchSchool/RB109/images/y_equal_x_y_reassign.jpg">

**Conceptually** in these examples, `=` says: _"If we're not referencing another variable, make a new object and put it in a new spot in memory."_

> **Clarification**:
> Note the emphasis on _"conceptually"_ in that last line...
> `=` doesn't always create a new object in memory, sometimes it only points to a new location in memory, but we'll get into that later in this article. For now, just know that the objects we've currently been working with, will create new objects with new locations in memory. 

---

# Non-Mutating

This concept of making a new object and giving it its own place in memory is known as _non-mutating_. 

It's named this way because we are **not** mutating or changing the object itself, we're simply creating a new object with a new location in memory.

`=` is a non-mutating operation. It does **not** change or mutate the object in memory, it creates a new object, with its own object ID.

Even if we're reassigning a variable to the exact same value, we'll be creating a brand new object with a new location in memory:
```ruby
x = "howdy"
x.object_id # Returns: 60

x = "howdy" 
x.object_id # Returns: 80
```
Notice how `x`'s address in memory changed, even though we reassigned it to the exact same value it had before.

#### To really drive home the point, you can think of the above example as such:

<img alt="Image of variables being represented as references" src="/Users/jacksebben/LaunchSchool/RB109/images/reassignment_to_the_same_value.jpg">

---

# Assignment & Reassignment

**Now, let's dive into the nuances of Non-Mutating...**

Consider this code:
```ruby
x = "howdy"

x.object_id # Returns: 60

x.upcase # Returns: "HOWDY"

x.object_id # Returns: 60

puts x # Outputs: howdy
```
> **`upcase` :**
> `upcase` is a method that will change all the letters in a value to uppercase.

**Notice:**
- How the object ID stays the same for `x` throughout the example (it points to the same location in memory)
- How on the final line, `x` still outputs `"howdy"`
- How `x.upcase` returns the value of "HOWDY"

In the above example, we **are not** mutating or changing the value of the object that `x` points to and we ****are not**** changing the location in memory that `x` points/references to.

**So what is happening here?**

`upcase` is a non-mutating method. Given our current definition, this means `upcase` is creating a new object in a new address in memory. This is just like our assignment/reassignment operator, `=`.

The only difference is, that `upcase` (unlike `=`) doesn't tell our caller variable (`x`) to point to that new object with a new address in memory - `upcase` is **just** returning that new object to us.

Let's use `object_id` to show what's happening:
```ruby
x = "howdy"

x.object_id # Returns: 60

x.upcase.object_id # Returns: 80

x.object_id # Returns: 60
```
As you can see, `x.upcase` is returning a newly made object "HOWDY" from the memory location of `80`, but is not reassigning `x`'s pointer to `80`. `upcase` is just returning you a value from the operation involving the caller variable, `x`.

```ruby
x = "howdy"

x.object_id # Returns: 60

x.upcase.object_id # Returns: 80
x.upcase.object_id # Returns: 100
x.upcase.object_id # Returns: 120

x.object_id # Returns: 60
```
As shown, calling `upcase` on a variable will make a new object in a new location each time it's called, but will not affect where the caller variable is pointing/referencing to.

> **Super Imporatant Note:**
>
> Assignment and Reassignment operations using operators like `=`; `+=`; `-=`; `*=`; `/=`; `%=`; `**=`, are non-mutating, but will change the pointer of the caller variable to point to a new location in memory.
>
> _Example_: `x *= 10` (the same as saying `x = x * 10`). `x` now points to a new location in memory containing the value of `x * 10`.
>
> Whereas, all other non-mutating methods like `upcase`, don't change the pointer of the caller variable.
>
> _Example_: `x.upcase` is non-mutating but ***returns*** the value of the operation. It **does not** change `x` to point to a new location in memory with the returned value of the operation.

---

# Mutating

***Mutating*** is the concept of changing or modifying an object in memory, but not changing its location in memory. The object persists in the same place in memory, but itself is modified.

Mutating **does not** change the variable referencing that object's pointer/reference in memory.

Here's an example to illustrate:
```ruby
x = "howdy"
x.upcase! # Mutates the object that `x` points to.

puts x # Outputs: HOWDY
```
> **`upcase!` :**
> The `upcase!` method is the mutating version of `upcase`. `upcase!` is different from the non-mutating `upcase` method that we used in previous examples.

As you can see, the object that `x` points to is mutated. When we output the value of `x` to the terminal, we can see that the value changed from it's originally assigned value of `"howdy"` to `"HOWDY"`. 

Let's use `object_id` to hit this one out of the park:
```ruby
x = "howdy"
puts x # Outputs: howdy
x.object_id # Returns: 60

x.upcase!
puts x # Outputs: HOWDY
x.object_id # Returns: 60
```
#### Our mental model for this one feels less eventful, but this is what a mutation looks like:

<img alt="Image of variables being represented as references" src="/Users/jacksebben/LaunchSchool/RB109/images/mutating_x.jpg">

`x` still points to the same location in memory, but the object itself has been modified.

> **It's important to note:**
> To understand what methods are mutating and non-mutating in Ruby can be tough. There are conventions that Ruby follows such as having a '!' at the end of a method's name, symbolizing that it is mutating. But these conventions are just guides and won't apply to all mutating methods. So it's important to test methods in order to find out whether or not they are mutating or non-mutating.

---

# Mutable VS Immutable Objects

Alright, here's the last weird nuance we'll explore.

Recap:
- Variables are references to objects
- Non-Mutating operations/methods create a new object in a new location in memory
- Assigment and reassignment operations are non-mutating, but change the reference of the variable to the newly made object.
- Mutating operations/methods modify or change an object in memory. There's no changes in an objects location in memory or the variable's reference.

Okay, now that we have that recap, we can dive into the concept of mutable and immutable objects.

## Immutable Objects:

Let's try out this code (guess whether the object IDs for both will be the same or not):
```ruby
num = 10

num = 10
```
Remember in our one example where we intialized variable `x` to reference `"howdy"` and then reassigned `x` to reference `"howdy"` again? We were able to observe that each assignment and reassignment creates a new object in a new location in memory.

Based on that alone, we might assume that our above example would yield the same results then? In both assignment and the reassignment `num` to `10` we should have different object IDs.

Let's find out:
```ruby
num = 10
num.object_id # Returns: 21

num = 10
num.object_id # Returns: 21
```
What?! "But, I thought `=` was non-mutating, meaning it would create a new object in a new location in memory??"

That only applies to mutable objects.
Immutable objects are objects in Ruby that cannot be mutated or changed.

Integers (Numbers) like `10`, are immutable. There is and will only ever be one single `10` object with its own place in memory. 

When we assign or reassign a variable to an immutable object, we are simply pointing the variable a location in memory where this object resides.

Here's assignment of multiple variables to the immutable object, `100`, with object IDs to show that they all share the same reference to the same object:
```ruby
num = 100
num2 = 100
num3 = 100

num.object_id  # Returns: 201
num2.object_id # Returns: 201
num3.object_id # Returns: 201
```

Here's our mental model for immutable objects:

<img alt="Image of variables being represented as references" src="/Users/jacksebben/LaunchSchool/RB109/images/immutable_objects.jpg">

When we perform an operation on an immutable object that ***appears*** to be mutable, it is not, it can't be. What's actually happening is the reassignment of the variable's reference to a different location in memory.

Other common data types in Ruby that are immutable include:
- Booleans
- Floats
- Symbols

> **Big Take-away:**
> _You cannot mutate nor are there any mutating methods for immutable objects._


## Mutable Objects:

Most of this article we've been dealing with mutable objects, these are objects in Ruby that can be mutated and changed. This is how we've been able to use methods like `upcase!` to change the objects our variables reference, without changing the variable's reference to a different object in a different place in memory.

Some common mutable data types in Ruby include:
- Strings
- Arrays
- Hashes