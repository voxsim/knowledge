# The Transformation Priority Premise

Refactorings have counterparts called Transformations. Refactorings are simple operations that change the structure of code without changing it’s behavior. Transformations are simple operations that change the behavior of code. Transformations can be used as the sole means for passing the currently failing test in the red/green/refactor cycle. Transformations have a priority, or a preferred ordering, which if maintained, by the ordering of the tests, will prevent impasses, or long outages in the red/green/refactor cycle.

```
“As the tests get more specific, the code gets more generic.”
```
