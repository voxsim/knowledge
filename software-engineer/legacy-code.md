
# The Legacy Code Change Algorithm 

When you have to make a change in a legacy code base, here is an algorithm you can use.

1. Identify change points.
2. Find test points.
3. Break dependencies.
4. Write tests.
5. Make changes and refactor.

One of the biggest challenges in getting legacy code under test is breaking dependencies. When we are lucky, the dependencies that we have are small and localized; but in pathological cases, they are numerous and spread out throughout a code base. The seam view of software helps us see the opportunities that are already in the code base. If we can replace behavior at seams, we can selectively exclude dependencies in our tests. We can also run other code where those dependencies were if we want to sense conditions in the code and write tests against those conditions. Often this work can help us get just enough tests in place to support more aggressive work.

A seam is a place where you can alter behavior in your program without editing in that place.

A seam can be a dependency of your software, a link to a package or a preprocessor if you use a compiler.

You can deal with a 

## Sprout method
When you need to add a feature to a system and it can be formulated completely as new code, write the code in a new method. Call it from the places where the new functionality needs to be.
Here are the steps that you actually take: 
1. Identify where you need to make your code change.
2. If the change can be formulated as a single sequence of statements in one place in a method, write down a call for a new method that will do the work involved and then comment it out. (I like to do this before I even write the method so that I can get a sense of what the method call will look like in context.)
3. Determine what local variables you need from the source method, and make them arguments to the call.
4. Determine whether the sprouted method will need to return values to source method. If so, change the call so that its return value is assigned to a variable.
5. Develop the sprout method using test-driven development.
6. Remove the comment in the source method to enable the call.

## Wrap Method
Wrap Method is a great way to introduce seams while adding new features. There are only a couple of downsides. The first is that the new feature that you add can’t be intertwined with the logic of the old feature. It has to be something that you do either before or after the old feature.

Here are the steps for the first version of the Wrap Method:
1. Identify a method you need to change.
2. If the change can be formulated as a single sequence of statements in one place, rename the method and then create a new method with the same name and signature as the old method. Remember to Preserve Signatures as you do this.
3. Place a call to the old method in the new method
4. Develop a method for the new feature, test first, and call it from the new method

In the second version, when we don’t care to use the same name as the old method, the steps look like this:
1. Identify a method you need to change.
2. If the change can be formulated as a single sequence of statements in one place, develop a new method for it using test-driven development.
3. Create another method that calls the new method and the old method.

For both sprout and wrap, you can do the same with classes and packages.

## The Method Use Rule
Before you use a method in a legacy system, check to see if there are tests for it. If there aren’t, write them. When you do this consistently, you use tests as a medium of communication. People can look at them and get a sense of what they can and cannot expect from the method. The act of making a class testable in itself tends to increase code quality. People can find out what works and how; they can change it, correct bugs, and move forward.

## Golden Master
TODO
