# Null Object Pattern

When you are writing tests and an object requires a parameter that is hard to construct, we often consider just to pass null.

If the parameter is used in the course of your test execution, the code will throw an exception and the test harness will catch the exception. If you need behavior that really requires an object, you can construct it and pass it as a parameter at that point.

The important thing to remember is this: Don’t pass null in production code unless you have no other choice.

If you are tempted to use null in production code, find the places where you are returning nulls and passing nulls, and consider a different protocol. Consider using the Null Object Pattern instead.

A Null Object Pattern is a class that answers to every method of the original class without doing nothing.
