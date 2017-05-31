Big O efficiency:

Operation | Average | Worst 
-------|---------|-------
Access | n/a     | n/a
Search | O(1)    | O(1)
Insert | O(1)    | O(n)
Delete | O(1)    | O(n)

A hash table is a data structure that maps keys to values for highly efficient lookup. In a very simple implementation of a hash table, the hash table has an underlying array and a hash function. When you want to insert an object and its key, the hash function maps the key to an integer, which indicates the index in the array. The object is then stored at that index.
Usually hash function generates values are almost unique, but sometimes collisions may happen.
A *hash collision* are when a hash function returns the same output for two distinct inputs: all hash functions have this problem and this is often accommodated for by having the hash tables be very large. 

Implementation in javascript inspired by [itsy-bitsy-data-structures](https://github.com/thejameskyle/itsy-bitsy-data-structures).

```javascript

class HashTable {

  constructor() {
    this.memory = [];
  }

  /**
   * Let's setup our "hashKey" function.
   *
   * Don't worry about understanding the logic of this function, just know that
   * it accepts a string and outputs a (mostly) unique address that we will use
   * in all of our other functions.
   */

  hashKey(key) {
    let hash = 0;
    for (let index = 0; index < key.length; index++) {
      // Oh look– magic.
      let code = key.charCodeAt(index);
      hash = ((hash << 5) - hash) + code | 0;
    }
    return hash;
  }

  /**
   * Next, let's define our "get" function so we have a way of accessing values
   * by their key.
   *
   * HashTable access is constant O(1) - "AWESOME!!"
   */

  get(key) {
    // We start by turning our key into an address.
    let address = this.hashKey(key);
    // Then we simply return whatever is at that address.
    return this.memory[address];
  }

  /**
   * We also need a way of adding data before we access it, so we will create
   * a "set" function that inserts values.
   *
   * HashTable setting is constant O(1) - "AWESOME!!"
   */

  set(key, value) {
    // Again we start by turning the key into an address.
    let address = this.hashKey(key);
    // Then just set the value at that address.
    this.memory[address] = value;
  }

  /**
   * Finally we just need a way to remove items from our hash table.
   *
   * HashTable deletion is constant O(1) - "AWESOME!!"
   */

  remove(key) {
    // As always, we hash the key to get an address.
    let address = this.hashKey(key);
    // Then, if it exists, we `delete` it.
    if (this.memory[address]) {
      delete this.memory[address];
    }
  }
}
```

Instead of making an extremely large array for storing objects at index `hash(key)`, we can make the array much smaller and store objects in a linked list at index `hash(key) % array_length`. To get the object with a particular key, we must search the linked list for the key.

Alternatively, we can implement the hash table with a binary search tree. We can then guarantee an O(log n) lookup time, since we keep the tree balanced. Aditionally we may use less space, since a large array no longer needs to be allocated in the very beginning.

Hash function
We can write:
- `((hash << 5) - hash) + code`
- `((hash * 32) - hash) + code`
- `hash * (1 * 32 - 1) + code`
- `hash * 31 + code`

The value 31 was chosen because it is an odd prime. If it were even and the multiplication overflowed, information would be lost, as multiplication by 2 is equivalent to shifting. The advantage of using a prime is less clear, but it is traditional. A nice property of 31 is that the multiplication can be replaced by a shift and a subtraction for better performance: 31 * i == (i << 5) - i. Modern VMs do this sort of optimization automatically.

You can also implement a Map with a Tree and search operation will be in O(logn) time.
