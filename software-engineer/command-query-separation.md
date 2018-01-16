# Command/Query Separation
Command/Query Separation is a design principle first described by Bertrand Meyer.

Simply put, it is this: A method should be a command or a query, but not both.

A command is a method that can modify the state of the object but that doesn’t return a value.

A query is a method that returns a value but that does not modify the object.

Why is this principle important?

There are a number of reasons, but the most primary is communication. If a method is a query, we shouldn’t have to look at its body to discover whether we can use it several times in a row without causing some side effect.
