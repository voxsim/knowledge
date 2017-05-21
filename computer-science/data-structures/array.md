Big O efficiency:
- Access:           array: O(1),      list: O(1)
- Search:           array: O(n),      list: O(n)
- Optimized Search: array: O(log n),  list: O(log n)
- Insertion:        array: n/a        list: O(n)
- Delete:           array: n/a        list: O(n)

A list/array is a representation of an ordered sequence of values where the same value may appear many times.
They are great for fast access and dealing with items at the end (i.e. they are bad at searching, inserting and deleting at beginning and middle).
Usually an array is a contiguous area of memory consisting of equal-size elements indexed by contiguous integers. They have fixed size. A list (or arraylist) is called also dynamic array and when is full, it copies its content to a larger array (the new array has usually double size of the original one).

Implementation in javascript inspired by [itsy-bitsy-data-structures](https://github.com/thejameskyle/itsy-bitsy-data-structures).

```javascript

class List {
  constructor() {
    this.memory = [];
    this.length = 0;
  }

  /**
   * First we need a way to retrieve data from our list.
   *
   * With a plain list, you have very fast memory access because you keep track
   * of the address directly.
   *
   * List access is constant O(1) - "AWESOME!!"
   */

  get(address) {
    return this.memory[address];
  }

  /**
   * Because lists have an order you can insert stuff at the start, middle,
   * or end of them.
   *
   * For our implementation we're going to focus on adding and removing values
   * at the start or end of our list with these four methods:
   *
   *   - Push    - Add value to the end
   *   - Pop     - Remove value from the end
   *   - Unshift - Add value to the start
   *   - Shift   - Remove value from the start
   */

  /*
   * Starting with "push" we need a way to add items to the end of the list.
   *
   * It is as simple as adding a value in the address after the end of our
   * list. Because we store the length this is easy to calculate. We just add
   * the value and increment our length.
   *
   * Pushing an item to the end of a list is constant O(1) - "AWESOME!!"
   */

  push(value) {
    this.memory[this.length] = value;
    this.length++;
  }

  /**
   * Next we need a way to "pop" items off of the end of our list.
   *
   * Similar to push all we need to do is remove the value at the address at
   * the end of our list. Then just decrement length.
   *
   * Popping an item from the end of a list is constant O(1) - "AWESOME!!"
   */

  pop() {
    if(this.length === 0) return;

    this.length--;
    let value = this.memory[this.length];
    delete this.memory[this.length];

    return value;
  }

  /**
   * In order to add a new item at the beginning of our list, we need to make
   * room for our value at the start by sliding all of the values over by one.
   *
   *     [a, b, c, d, e]
   *      0  1  2  3  4
   *       ⬊  ⬊  ⬊  ⬊  ⬊
   *         1  2  3  4  5
   *     [x, a, b, c, d, e]
   *
   * In order to slide all of the items over we need to iterate over each one
   * moving the prev value over.
   *
   * Because we have to iterate over every single item in the list:
   *
   * Unshifting an item to the start of a list is linear O(N) - "OKAY."
   */

  unshift(value) {
    this.memory = [value, ...this.memory];
    this.length++;
  }

  /**
   * Finally, we need to write a shift function to move in the opposite
   * direction.
   *
   * We delete the first value and then slide through every single item in the
   * list to move it down one address.
   *
   *     [x, a, b, c, d, e]
   *         1  2  3  4  5
   *       ⬋  ⬋  ⬋  ⬋  ⬋
   *      0  1  2  3  4
   *     [a, b, c, d, e]
   *
   * Shifting an item from the start of a list is linear O(N) - "OKAY."
   */

  shift() {
    if(this.length === 0) return;

    let value = this.memory[0];
    [_, ...this.memory] = this.memory;
    this.length--;

    return value;
  }
}
```
