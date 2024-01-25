# Mutating VS Non-Mutating Methods in Ruby - The Confusing Parts

Here's where beginner, intermediate and even experienced devs slip up.

What is, understanding mutation of objects in OOP.

For this article, exmaples will be written and given in Ruby because of it's super readable syntax, but the concepts generally apply to most other OOP languages like JavaScript, Python, Java, Pearl and so on...

So even if you're not learning Ruby, you can join along and get a better understanding for the OOP language you're coding in.

## The Mental Model You'll Need To Learn This Concept

In my last article on Variables in Ruby (and OOP in general), I covered what variables ***actually*** are and the best way to think of them. 

I defined variables as:

_"- **references** to objects in memory."_

As a mental model, variables should look like this to you:

<img alt="Image of variables being represented as references" src="/Users/jacksebben/LaunchSchool/RB109/images/variables_as_references.jpg">

They're references that point to a location in memory that contains an object.

---

## Assignment and Reassignment

What happens when we initialize a variable, _like this_?
```ruby
x = "howdy"
```

Some might answer:
_"We're creating a reference that points to a new slot in memory with the newly made object, `"howdy"`."_


And, in this example we just gave above, you would be correct.

But what happens when we _do this?_:
```ruby
x = "howdy"
y = "howdy"
```
Two questions:
- Is `y` pointing to the same slot in memory as `x`?
- Is the object that `y` points to the same object that `x` points to (`"howdy"`)?

Why don't we find out?
```ruby
x = "howdy"
y = "howdy"

x += "!!"

puts y # Outputs: howdy
puts x # Outputs: howdy!!
```
> **For clarity:** In this example, `+=` is used to concatenate the sub-string (`"!!"`) onto the caller object (`x`).
> `x += "!"` is the same as saying: `x = x + "!"`

In the above example you can see that we changed the value of `x` by adding `!!` to the end of it. 

If `x` and `y` both referenced the same location in memory then changes to the value of `x` would've changed the value of `y`, given that we're referencing the same location in memory with the same object.

And we can see in the example above, that `y` is still pointing to the value `"howdy"` while `x` points to the value `"howdy!!"`

We can use the method `object_id` to further confirm this:
> `object_id` is a method that shows the "memory address" of an object. This method will return to us the address of the location in memory that the caller object is pointing to.
```ruby
x = "howdy"
y = "howdy"

x.object_id # returns: 60
y.object_id # returns: 80
```
> On my machine these are the "addresses" returned, on your machine they might be different than `60` and `80`. I'm not sure how Ruby decides where things or stored or what addresses to give them. The point still stands though and regardless, `x` and `y` on your machine should have different return values when `object_id` is called on them.

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
#### As you can see above, `x` and `y` have the same "memory addresses", meaning they both point to the same location in memory, containing the same object.

<img alt="Image of variables being represented as references" src="/Users/jacksebben/LaunchSchool/RB109/images/x_y_same_slot.jpg">

> **Important to note:**
> `x` and `y` are **not** sharing a pointer/reference, they are two separate pointers that point to the same location in memory.

---

## Where The Confusion Begins

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
In this case, the reassignment of `y` should've changed the object that `x` and `y` both point to. Why isn't `x` returning `"sup?"` ?

This is where the concept of Mutating VS Non-Mutating methods is introduced.

But first, let's see what happened to the object ID's in our last example:
```ruby
x = "howdy"
y = x

y = "sup?"

x.object_id # Returns: 60
y.object_id # Returns: 80
```

We can see that originally in the first 2 lines that `x` and `y` both reference the same location in memory (this is what `object_id` on my machine is calling `60`).

But on our reassignment of `y` to `"sup?"`, `y` now references a different location in memory. Our reassignment has created a new object in a new location.

#### Using our mental model, you can think of it like this:

<img alt="Image of variables being represented as references" src="/Users/jacksebben/LaunchSchool/RB109/images/y_equal_x_y_reassign.jpg">

Conceptually `=` says: _"If we're not referencing another variable, make a new object and put it in a new spot in memory."_

---

## Mutating VS Non-Mutating

This concept of making a new object and giving it its own place in memory is known as _non-mutating_. 

It's named this way because we are **not** mutating or changing the object itself, we're simply creating a new object with a new location in memory.

`=` is a non-mutating operation. It does **not** change or mutate the object in memory, it creates a new object, with it's own object ID.

Even if we're reassigning a variable to the exact same value, we'll be creating a brand new object with a new location in memory:
```ruby
x = "howdy"
x.object_id # Returns: 60

x = "howdy" 
x.object_id # Reutrns: 80
```
Notice how `x`'s address in memory changed, even though we reassigned it to the exact same value it had before.

#### To really drive home the point, you can think of the above example as such:

<img alt="Image of variables being represented as references" src="/Users/jacksebben/LaunchSchool/RB109/images/reassignment_to_the_same_value.jpg">