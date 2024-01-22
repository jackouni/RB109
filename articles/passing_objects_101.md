# How Objects Are Passed Around in Ruby And Other OOP Languages

### Table of Contents
- The Best Way to Think of Variables
- What are Blocks?
- Are You Reassigning a Variable Or Mutating a Value?
- Scoping Rules of Variables, Blocks and Methods
- Pass By Reference 🆚 Pass By Value
- Mutating 🆚 Non-Mutating Methods
- How Object Passing Truly Works - Call By Sharing

---

## How is data passed around in an application?

This is possibly one of the most important topics to be covered when learning the fundamentals of Ruby (and any programming langauge for that matter).

It's easy to see the abstractions and be shown how to pass objects to methods, or how a variable is made, or how to pass a block to a method...

But it doesn't exactly explain _why_ or _how_ the underlying mechanisms work. Not learning these principles can (and most likely will) lead to confusion, more debugging and more _hacking and slashing_.

You'll eventually be held up not knowing why:
- a method isn't returning the value you want
- why a method or block is or isn't modifying an object you passed it
- why a method or block is or isn't modifying an object you referenced in it


With this article, you'll be better set up for success when you encounter these scenarios and hopefully you won't have to encounter them as much. By knowing how data is passed around in Ruby and stripping back the layers of abstraction, we can avoid some of the (what seem like) "_quirks_" of Ruby.

***This isn't just for Ruby though!***

Most of the concepts covered in this article have strong cross-over with other programming languages like:

_Python, JavaScript, Java, Pearl, Smalltalk and more..._

So regardless of whatever OOP language you're writing in, this article will definitely give you a deeper understanding of "_object-passing_" in general.

---

## The Best Way to Think of Variables

Variables are used all the time in programming, and no matter what level you're at, you'll have used a variable. It's the first thing you usually learn about.

Most basic definitions for variables go something like this:
> _"Variables are used to store values in programming._
>
> An Example: 
>```ruby 
>x = 3
>```
> _Here our variable `x` is holding/storing the value `3` in it. Now when you reference `x` you'll access the value `3`."_

This is actually an okay way to teach beginners about variables. We're abstracting it down to some pretty simple terms that are easier to understand and help the beginner get going with their programming journey.

But it's not quite accurate, and won't benefit you in the longer run.


At this stage variables might be seen as a _"container"_ holding a value, like this:

<img alt="Image of a variable being represented as a container" src="/Users/jacksebben/LaunchSchool/RB109/images/variables_as_containers.jpg">


You reference a variable-container and it gives you the value it holds.
