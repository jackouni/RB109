# Launch School's Live Sessions: Part 3
> [Launch School Live Session: Beginning Ruby Part 3](https://launchschool.medium.com/live-session-beginning-ruby-part-3-61180782f721)

## Topics Covered in This File 📋

- Variables as Pointers
- Arrays 🆚 Hashes
  - What they are
  - How to retrieve/access items from them
- Iterators
  - Defining _Loops_, _Blocks_, and _Iterators_

<br>

--------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------

## Variables as Pointers to Objects 👉
In Ruby variables should be thought of as pointers that point to objects in memory. </br>
They should not be thought of as containers that hold objects. </br>
<br>

_**To reiterate:**_ </br>
Variables are used to point you to an object for referencing. </br>
They don't _hold_ objects in memory, they point to the spots in memory that hold objects.

<br>

--------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------


## Differences: Arrays 🆚 Hashes 
#### Arrays:
- Are a collection of indexed objects 
- Maintain an order starting from `0` index, `1` index and so on...
- Retrieve an object using the index it's located at in the array
- Arrays can have duplicate values

#### Hashes:
- Are a collection of objects paired with a 'key'
- Rely less on order. Objects in the Hash are referenced by a 'key'
- Retrieve an object using the 'key' that references it
- The 'keys' in a Hash are unique and CAN'T be duplicated.
<br>

#### Retrieval of Items:
_Arrays:_
```ruby
arr = [2, 4, 6, 8, 10]

arr[0] #=> 2
arr[1] #=> 4
arr[2] #=> 6
arr[4] #=> 10
```
_Hashes:_
```ruby
hash = {a: 2, b: 4, c: 6, d: 8, e: 10}

# Referencing keys:
hash[:a] #=> 2
hash[:b] #=> 4
hash[:c] #=> 6
hash[:e] #=> 10

# Using `fetch`
hash.fetch(:a) #=> 2
hash.fetch(:c) #=> 6
hash.fetch(:e) #=> 10
```
> _**To Note**_ 📝 </br>
> #### Accessing a hash value using square bracket notation V.S. `fetch`: </br>
> With **square brackets**, even if you insert a key that does not exist, the square brackets will return `nil` to you. </br>
> This can cause some confusion in your application when trying to debug. </br>
> Often times we want to avoid the returning of `nil`.</br>
> <br>
> With **`fetch`**, if you insert a key that doesn't exist it will throw an error. This is nice because this means we can avoid returning `nil` and be more aware of error-prone code we write. 
>
> _Example:_
> ```ruby
> hash = {a: 2, b: 4, c: 6, d: 8, e: 10}
>
> p hash[:f] #=> nil
> p hash.fetch(:f) #=> Will throw an error
> ```
<br>

---------------------------------------------------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------------------------------------------------

## Iterators 🔄

### Defining Terms 📖
- _**Iterators**_
  > Are methods in Ruby that allow us to iterate through the items in a collection (Arrays and Hashes). These methods keep us from having continue writing out our own loops repetitively. </br>
  With the use of blocks, iterators can allow us to inject our own custom logic into the iterative loop. </br>
  These iterators can make our code more concise and readable. </br>
  _Some common examples include:_ </br>
  > - `Array#map`
  > - `Array#each` / `Hash#each`
  > - `Array#select` / `Hash#select`
  > - `Hash#each_key` 
  > - `Hash#each_value`
  >
  > These are all examples of methods that perform some sort of iteration over the elements in a collection in order to achieve a certain result or return value.
<br>

- _**Blocks**_
  > A block is code that is passed to a method at invocation. </br>
  Code in a block is contained between either: </br>
  > 1. A `do/end` (multi-line)
  > 2. Curly braces, `{}` (one-liner) 
  >
  > Blocks can be thought of as "arguments" to methods, although not technically true. Blocks are a way to pass code to a method (much like how we pass objects as arguments to methods). </br>
  > Blocks are verys similar conceptually to the idea of '_callbacks_' in other languages like JavaScript. </br>
  > <br>
  >
  >  _Here's an example of implementing a block into a method and then invoking that block:_
  >```ruby
  > arr = [1, 3, 6, 9, 12, 15]
  >
  > def my_map(array)
  >  i = 0
  >  new_array = []
  >
  >  loop do
  >    item = array[i]
  >    new_array << yield(item) # Where we hand control over to the block
  >    i += 1
  >    break if i == array.size
  >   end
  >      
  >  new_array
  > end 
  >
  >
  >p my_map(arr) { |x| x * 2 } # `x` represents `item` from our method definition
  ># => [2, 6, 12, 18, 24, 30]
  >```

- _**Loops**_
  > Loops are a way to execute code multiple times consecutively, depending on certain logic. </br>
  > <br>
  > _Loops are blocks of code defined by (in order):_
  > - a 'looping' keyword (like `loop`, `while`, `until` ... etc)
  > - a **_condition_** (unless the loop is defined by the `loop` keyword) 
  > - By **_the code_** contained/wrapped between a `do/end`.
  >
  >**_The code_** defined in the loop will execute over and over again until the **_condition_** is met or if the `break` keyword is invoked within the loop definition.

<br>

---------------------------------------------------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------------------------------------------------

## Practice Problems From The Video 💪

Here's the Array we're working with: `arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]` </br>
Here's the Hash we're working with: `hsh = {a:1, b:2, c:3, d:4}`</br>
<br>

1. Iterate over each number in `arr` and print out its value - Loop V.S. Iteration
    <details>
    <summary> Answer </summary>

    _**Loop Answer:**_
    ```ruby
    arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

    ind = 0 
    loop do
      break if ind == arr.size
      puts arr[ind]
      ind += 1
    end
    ```
    _**Iteration Answer:**_
    ```ruby
    arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

    arr.each { |num| puts num }
    ```
    </details>
  <br>
  
2. Same as above, but only print numbers greater than 5
    <details>
    <summary> Answer </summary>

    _**Loop Answer:**_
    ```ruby
    arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

    ind = 0 
    loop do
      break if ind == arr.size
      puts arr[ind] if arr[ind] > 5
      ind += 1
    end
    ```
    _**Iteration Answer:**_
    ```ruby
    arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

    arr.each { |num| puts num if num > 5}
    ```
    </details>
  <br>

3. Append `12` to the end of `arr`
    <details>
    <summary> Answer </summary>

    ```ruby
    arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    arr << 12
    ```
    </details>
  <br>

4. Prepend `0` to the beginning of `arr`
    <details>
    <summary> Answer </summary>

    ```ruby
    arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    arr.unshift(0)
    ```
    </details>
  <br>

5. Remove `12` and add `3` from `arr`
    <details>
    <summary> Answer </summary>

    ```ruby
    arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 12]
    arr.pop
    arr << 3
    ```
    </details>
  <br>

6. Remove duplicates from `arr` using 1 method (no loop or iteration)
    <details>
    <summary> Answer </summary>

    ```ruby
    arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 3]
    arr.uniq!
    ```
    </details>
  <br>

7. Extract all odd numbers from `arr` into a new array. </br>
    <details>
    <summary> Answer </summary>

    ```ruby
    arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    arr.select { |num| num.odd? }
    ```
    </details>
  <br>

8. Increment all numbers in `arr` by 1 - Mutation V.S. Non-Mutation. </br>
    <details>
    <summary> Answer </summary>
    
    _**Mutating:**_ </br>
    ```ruby
    arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    arr.map! { |num| num + 1 }
    ```
    _**Non-Mutating:**_ </br>
    ```ruby
    arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    arr.map { |num| num + 1 }
    ```
    </details>
  <br>

9. Get the value of `:b` from `hsh`
    <details>
    <summary> Answer </summary>

    ```ruby
    hsh = {a:1, b:2, c:3, d:4}
    
    # Using square bracket notation:
    hsh[:b]

    # Using `fetch`:
    hsh.fetch(:b)
    ```
    </details>
  <br>

10. Add this key-value pair to `hsh`: `{:e => 5}`
    <details>
    <summary> Answer </summary>

    ```ruby
    hsh = {a:1, b:2, c:3, d:4}
    hsh[:e] = 5
    ```
    </details>
  <br>

11. Iterate over each key-value in `hsh` and print out each key and value
    <details>
    <summary> Answer </summary>

    ```ruby
    hsh = {a:1, b:2, c:3, d:4, e:5}
    hsh.each do |key, value|
      puts "Key: #{key}; Value: #{value};"
    end 
    ```
    </details>
  <br>

12. Same as above except only print out each key and value if the value is less than `3.5`
    <details>
    <summary> Answer </summary>

    ```ruby
    hsh = {a:1, b:2, c:3, d:4, e:5}
    hsh.each do |key, value|
      puts "Key: #{key}; Value: #{value};" if value < 3.5
    end 
    ```
    </details>
  <br>

13. Return a new Hash from `hsh` of the key-values where values are less than `3.5`
    <details>
    <summary> Answer </summary>

    ```ruby
    hsh = {a:1, b:2, c:3, d:4, e:5}
    small_vals = hsh.select do |key, value|
                  value < 3.5
                 end 
    ```
    </details>
  <br>

13. Delete all key-value pairs in `hsh` where value is less than 3.5
    <details>
    <summary> Answer </summary>

    ```ruby
    hsh = {a:1, b:2, c:3, d:4, e:5}
    hsh.delete_if! { |key, value| value < 3.5}
    ```
    </details>
  <br>

---------------------------------------------------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------------------------------------------------

## One of The Biggest Mistakes Beginners Make

According to the founder or Launch School, Chris Lee, one of the common mistakes beginners make when using methods is not having a good definition. </br>
<br>
When using methods, make sure you have a good definition of what that method does. </br>
_**Does it...?**_
- Mutate the Caller?
- Return a meaningful value/object?
- Return a boolean?
<br>

_**If iteration, is it...?**_ 
- Returning the last evaluated expression in a block?
- Returning the item from blocks that return a certain boolean (`true`/`false`)?
- Returning a boolean based on a certain conditional being or not being met?
<br>
<br>

These are all things to consider when using a method. 
If you have trouble explaining what the method does, 
it starts you off on rocky grounds and may make it harder for you to debug if ever you encounter a problem with that method. 