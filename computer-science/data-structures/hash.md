A hash table is a data structure that maps keys to values for highly efficient lookup. In a very simple implementation of a hash table, the hash table has an underlying array and a hash function. When you want to insert an object and its key, the hash function maps the key to an integer, which indicates the index in the array. The object is then stored at that index.

Implementation in javascript inspired by [itsy-bitsy-data-structures](https://github.com/thejameskyle/itsy-bitsy-data-structures).

```javascript

class HashTable {

  constructor() {
    this.memory = [];
  }

  /**
   * In order to store key-value pairs in memory from our hash table we need a
   * way to take the key and turn it into an address. We do this through an
   * operation known as "hashing".
   *
   * Basically it takes a key and serializes it into a unique number for that
   * key.
   *
   *    hashKey("abc") =>  96354
   *    hashKey("xyz") => 119193
   *
   * You have to be careful though, if you had a really big key you don't want
   * to match it to a memory address that does not exist.
   *
   * So the hashing algorithm needs to limit the size, which means that there
   * are a limited number of addresses for an unlimited number of values.
   *
   * The result is that you can end up with collisions. Places where two keys
   * get turned into the same address.
   *
   * Any real world hash table implementation would have to deal with this,
   * however we are just going to glaze over it and pretend that doesn't happen.
   */

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
