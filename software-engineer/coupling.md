# Coupling

Coupling refers to the degree to which components in your program rely on each other. You should generally seek to minimize this property, though you’ll see it’s impossible to eliminate entirely.

Here are a few types of coupling, ordered by severity (first is worst):

## Pathological Coupling
Your class reaches inside another class and reads (or, perish the thought, changes) its instance variables. Monkey-patching falls into this category.

## Global Coupling
You have two classes that both rely on some shared global data, maybe a Singleton or a class variable.

## Control Coupling
You pass in a flag that tells a method what to do. Control couples are smelly because the calling method has intimate knowledge of how the receiver implements the method being called.

## Data Coupling
You call a method and pass it a parameter that doesn’t affect its control flow.

## Message Coupling
You’re coupled to the name of the message, but not any hint of its implementation. This is the loosest type of coupling and should be your goal. Notice that this makes methods that take no arguments better than methods that take one (and so on).
