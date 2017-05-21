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

Questions:
1. A child is running up a staircase with n steps, and can hop either 1 step, 2 steps or 3 steps at a time. Implement a method to count how many possible ways the child can run up the stairs.
2. Write a program that prints all permutations of a string of unique characters.
3. Implement an algorithm to print all valid combinations of n-pairs of parentheses
4. Given a quarter (25 cents), dimes (10 cents), nickels (5 cents) and pennies (1 cent). Write code to calculate the number of ways of representing n cents.
