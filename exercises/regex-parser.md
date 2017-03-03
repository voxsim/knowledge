# Regex Parser

Implement a simple regex parser which, given a string and a pattern, returns a boolean indicating whether the input matches the pattern.

## Requirements

1. Include "." which stands for 1 exact character
2. Include "*" which stands for 0 or more characters
3. Include "+" which stands for 1 or more characters
4. Multiple consecutive 'special characters' are allowed.
5. You can look precisely for a 'special character' if you escape it: add a '\' before.

## Step notes

1. Test it against empty or null string. Do you see other corner cases?
2. Write the solution using the recursion
3. Write the solution using an iterative approach
4. Write the solution using an object-oriented approach. Remember oop is more about comunication between objects, try to implement each requirement:
  - Following the Open-Closed Principle
  - Don't break the encapsulation of each object
  - Avoid the use of getters / setters
5. Write the solution in a functional way, do you see some differences from the point 2?
