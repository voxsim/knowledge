# Array

*   Array inherits from Object
*   Indexes are converted to strings and used as names for retrieving values
*   Very efficient for sparse array
*   Not very efficient in most of other cases
*   One advantage: No need to provide a length or type when creating an array
*   Literal form: []
*   It can contain any number of expressions separated by commas
*   New items can be appendend
*   The dot notation should be not used by arrays

sort myArray: -> it sorts alphabetically (everything number too, but we can pass a function in sort)

delete myArray[1]; -> it puts undefined in number 1 index; -> we need to use splice to delete the element and resize the array

## Array.from
`Array.from(arrayLike[, mapFn[, thisArg]])` method creates a new Array instance from an array-like or iterable object.

```javascript
const bar = ["a", "b", "c"];
Array.from(bar);
// ["a", "b", "c"]

Array.from('foo');
// ["f", "o", "o"]

// Using an arrow function as the map function to
// manipulate the elements
Array.from([1, 2, 3], x => x + x);      
// [2, 4, 6]


// Generate a sequence of numbers
// Since the array is initialized with `undefined` on each position,
// the value of `v` below will be `undefined`
Array.from({length: 5}, (v, i) => i);
// [0, 1, 2, 3, 4]
```

## Array.isArray
The `Array.isArray(obj)` function determines whether the passed value is an Array

```javascript
// all following calls return true
Array.isArray([]);
Array.isArray([1]);
Array.isArray(new Array());
// Little known fact: Array.prototype itself is an array:
Array.isArray(Array.prototype); 

// all following calls return false
Array.isArray();
Array.isArray({});
Array.isArray(null);
Array.isArray(undefined);
Array.isArray(17);
Array.isArray('Array');
Array.isArray(true);
Array.isArray(false);
Array.isArray({ __proto__: Array.prototype });
```

## Array.of
The `Array.of(element0[, element1[, ...[, elementN]]])` method creates a new Array instance with a variable number of arguments, regardless of number or type of the arguments.

## Array.prototype.concat
The concat() method is used to merge two or more arrays. This method does not change the existing arrays, but instead returns a new array.

## Array.prototype.entries
The entries() method returns a new Array Iterator object that contains the key/value pairs for each index in the array.

## Array.prototype.every / Array.prototype.some
The every() method tests whether all/some elements in the array pass the test implemented by the provided function

```javascript
function isBigEnough(element, index, array) { 
  return element >= 10; 
} 

[12, 5, 8, 130, 44].every(isBigEnough);   // false 
[12, 54, 18, 130, 44].every(isBigEnough); // true
```

## Array.prototype.filter
The `var newArray = arr.filter(callback[, thisArg])` method creates a new array with all elements that pass the test implemented by the provided function.

```javascript
var words = ["spray", "limit", "elite", "exuberant", "destruction", "present"];

var longWords = words.filter(function(word){
  return word.length > 6;
});

// Filtered array longWords is ["exuberant", "destruction", "present"]
```

## Array.prototype.map
The map() method creates a new array with the results of calling a provided function on every element in the calling array

```javascript
var numbers = [1, 5, 10, 15];
var doubles = numbers.map(function(x) {
   return x * 2;
});
// doubles is now [2, 10, 20, 30]
// numbers is still [1, 5, 10, 15]

var numbers = [1, 4, 9];
var roots = numbers.map(Math.sqrt);
// roots is now [1, 2, 3]
// numbers is still [1, 4, 9]
```

## Array.prototype.reduce
The reduce(accumulator(accumulator, currentValue, currentIndex)[, initialValue]) method applies a function against an accumulator and each element in the array (from left to right) to reduce it to a single value.

var total = [0, 1, 2, 3].reduce(function(sum, value) {
  return sum + value;
}, 0);
// total is 6

var flattened = [[0, 1], [2, 3], [4, 5]].reduce(function(a, b) {
  return a.concat(b);
}, []);
// flattened is [0, 1, 2, 3, 4, 5]

## Array.prototype.slice
The `slice([, start[, end]])`  method returns a shallow copy of a portion of an array into a new array object selected from begin to end (end not included). The original array will not be modified.
