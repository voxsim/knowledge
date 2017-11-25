An algorithm that calls itself in its definition.
- *Recursive case* a conditional statement that is used to trigger the recursion.
- *Base case* a conditional statement that is used to break the recursion.

What you need to know:
- *Stack level too deep* and *stack overflow*.
  - If you've seen either of these from a recursive algorithm, you messed up.
  - It means that your base case was never triggered because it was faulty or the problem was so massive you ran out of RAM before reaching it.
  - Knowing whether or not you will reach a base case is integral to correctly using recursion.
  - Often used in Depth First Search

```                         
recursive method (array, n)
  if array[n] is not nil
    print array[n]
    recursive method(array, n+1)
  else                     
    exit loop
```

Recursion Vs. Iteration
- The differences between recursion and iteration can be confusing to distinguish since both can be used to implement the other. But know that,
  - Recursion is, usually, more expressive and easier to implement.
  - Iteration uses less memory.
- **Functional languages** tend to use recursion. (i.e. Haskell)
- **Imperative languages** tend to use iteration. (i.e. Ruby)
