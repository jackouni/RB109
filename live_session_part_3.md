bb# Launch School's Live Sessions: Part 3
> [Launch School Live Session: Beginning Ruby Part 3](https://launchschool.medium.com/live-session-beginning-ruby-part-3-61180782f721)

<br>

## Variables as Pointers to Objects:
In Ruby variables should be thought of as pointers that point to objects in memory. </br>
They should not be thought of as containers that hold objects. </br>
_To reiterate:_ </br>
Variables are used to point you to an object for referencing. </br>
They don't _hold_ objects in memory, they point to the spots in memory that hold objects.

<br>
<hr>

## Differences Between Arrays and Hashes:
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