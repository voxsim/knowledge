# Currying
A common technique in FP is currying. Currying is the process of converting a function that
takes multiple arguments into a function that takes one argument at a time, returning
another function.

Let's look at an example to clarify the concept.
Instead of writing:
```javascript
const add = (x, y) => x + y
```

We define the function like this:
```javascript
const add = x => y => x + y
```

And we use it in the following way:
```javascript
constadd1 = add(1)
add1(2) // 3
add1(3) // 4
```

This is a pretty convenient way of writing functions because since the first value is stored after the application of the first parameter, we can reuse the second function multiple times.
