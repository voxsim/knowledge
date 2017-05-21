Big O efficiency:

Operation | Average | Worst 
-------|---------|-------
Access | n/a     | n/a    
Search | O(1)    | O(1)  
Insert | O(1)    | O(n)  
Delete | O(1)    | O(n)  

A hash table is a data structure that maps keys to values for highly efficient lookup. In a very simple implementation of a hash table, the hash table has an underlying array and a hash function. When you want to insert an object and its key, the hash function maps the key to an integer, which indicates the index in the array. The object is then stored at that index.
A *hash collision* are when a hash function returns the same output for two distinct inputs: All hash functions have this problem and this is often accommodated for by having the hash tables be very large.

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

From TopCoder:
Hash tables are a unique data structure, and are typically used to implement a "dictionary" interface, whereby a set of keys each has an associated value. The key is used as an index to locate the associated values. This is not unlike a classical dictionary, where someone can find a definition (value) of a given word (key). 

Unfortunately, not every type of data is quite as easy to sort as a simple dictionary word, and this is where the "hash" comes into play. Hashing is the process of generating a key value (in this case, typically a 32 or 64 bit integer) from a piece of data. This hash value then becomes a basis for organizing and sorting the data. The hash value might be the first n bits of data, the last n bits of data, a modulus of the value, or in some cases, a more complicated function. Using the hash value, different "hash buckets" can be set up to store data. If the hash values are distributed evenly (which is the case for an ideal hash algorithm), then the buckets will tend to fill up evenly, and in many cases, most buckets will have no more than one or only a few objects in them. This makes the search even faster. 

A hash bucket containing more than one value is known as a "collision". The exact nature of collision handling is implementation specific, and is crucial to the performance of the hash table. One of the simplest methods is to implement a structure like a linked list at the hash bucket level, so that elements with the same hash value can be chained together at the proper location. Other, more complicated schemes may involve utilizing adjacent, unused locations in the table, or re-hashing the hash value to obtain a new value. As always, there are good and bad performance considerations (regarding time, size, and complexity) with any approach. 

Another good example of a hash table is the Dewey decimal system, used in many libraries. Every book is assigned a number, based upon its subject matterï¿½ the 500′s are all science books, the 700′s are all the arts, etc. Much like a real hash table, the speed at which a person could find a given book is based upon how well the hash buckets are evenly dividedï¿½ It will take longer to find a book about frogs in a library with many science materials than in a library consisting mostly of classical literature. 

In applications development, hash tables are a convenient place to store reference data, like state abbreviations that link to full state names. In problem solving, hash tables are useful for implementing a divide-and-conquer approach to knapsack-type problems. In LongPipes, we are asked to find the minimum number of pipes needed to construct a single pipe of a given length, and we have up to 38 pieces of pipe. By dividing this into two sets of 19, and calculating all possible lengths from each set, we create hash tables linking the length of the pipe to the fewest number of segments used. Then, for each constructed pipe in one set, we can easily look up, whether or not we constructed a pipe of corresponding length in the other set, such that the two join to form a complete pipe of the desired length.

Questions:
1. Implement and explain how an hash function
2. Why the worst case for insert/delete is O(n) for an hash table?
3. What are and why the worst operations for an hash table
4. Can you implement a Map with a tree? What about with a list?
