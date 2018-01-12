# Separation of concerns


When we have to change the behavior of a system, we want to change as little code as possible.

If all the relevant changes are in one area of code, we don’t have to hunt around the system to get the job done.

Because we cannot predict when we will have to change any particular part of the system, we gather together code that will change for the same reason.

For example, code to unpack messages from an Internet standard protocol will not change for the same reasons as business code that interprets those messages, so we partition the two concepts into different packages.
