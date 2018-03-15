# Lazy Evaluation
Combining functions allows strict synchronisation between them to the point where a computation only happens when the result is really required and suspended until another value is needed. This allows for possibly infinite streams of values that will be evaluated on demand decoupling looping from termination conditions for a more modular design. Again silver bullets don’t exist and while lazy evaluation frees the developer’s mind from having to control the execution flow when applied to referential transparent expressions, it makes it more challenging to understand when applied on side effects defeating the modularity that was designed to provide.