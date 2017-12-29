## Testability
What the codes does is irrelevant; how the code is structured is all that matters for testability. Testable code means properly managed the dependencies.

## Hard to test in code
- Mixing creation/new in logic
- Looking for things
- Work in constructor
- Global state
- Singleton
- static methods
- Implicit dependencies
- Deep inheritance
- Too many conditionals
- Mixing service/value
- Mixing concerns
- etc..

## Kind of tests for developer
- Acceptance / Scenario tests: test the whole system pretends to be an user
- Functional tests: test collection of classes as subsystems
- Integration tests: test the integration between your system and an external one
- Unit tests: test individual classes / methods in isolation

They are ordered from the bigger execution time to fewer, they are also ordered by scope frome huge to small.

### Integration tests

One of the most common cases of using a TestDouble is when you are communicating with an external service. Typically such services are being maintained by a different team, they may be subject to slow, and unreliable networks, and maybe unreliable themselves. That's why a test double is handy, it stops your own tests from being slow and unreliable. 

A good way to deal with this is to run your own tests against the double, but to periodically run a separate set of integration contract tests that checks all the calls against your test doubles return the same results as a call to the external service would. A failure in any of these integration contract tests implies you need to update your test doubles, and probably your code to take into account the service contract change.

These tests need not be run as part of your regular deployment pipeline. Your regular pipeline is based on the rhythm of changes to your code, but these tests need to be based on the rhythm of changes to the external service. Often running just once a day is plenty.

A failure in an integration contract test shouldn't necessarily break the build in the same way that a normal test failure would. It should, however, trigger a task to get things consistent again. This may involve updating the tests and code to bring them back into consistency with the external service. Just as likely it will trigger a conversation with the keepers of the external service to talk about the change and alert them to how their changes are affecting other applications.

This communication with the external service supplier is even more important if this service is being used as part of a production application. In these cases an integration contract change may break a production application, triggering an emergency fix and an urgent conversation with the supplier team.

## Tests like a black box
It must be easier write the test and see test result and after writing the application. We should refactoring without have brittle tests and we should even delete the code and rewrite the application if we write the tests in a good way.
Every test should told us a story.

## Edge cases
Based on the content of the algorithm you can identify what data structures/types/constructs are used. Then, you try to understand the (possible) weak points of those and try to come up with an execution plan that will make it run in those cases.

For example, the algorithm takes a string and an integer as input and does some sorting of the characters of the string.

Here we have:

String with some known special cases:

Empty string
Long string
Unicode string (special characters)
If limited to a specific set of characters, what happens when some are not in the range
Odd/even length string
Null (as argument)
Non-null terminated
Integer with known special cases:

0
Min/MaxInt
Negative/Positive
Sort algorithm that could fail in the following boundary cases:

Empty input
1 element input
Very long input (maybe of length max(data type used for index))
Garbage inside the collection that will be sorted
Null input
Duplicate elements
Collection with all elements equal
Odd/even length input
Then, take all these cases and create a long list trying to understand how they overlap. Ex:

Empty string case covers the empty collection case
Null string == null collection
etc.
Now create test cases for them :)

Short summary: break the algorithm in basic blocks for which you know the boundary cases and then reassemble them, creating global boundary cases

## Function
To test a function:

1. Define tests cases
   - Normal cases
   - Edge cases
     - Extremes
     - Nulls and illegal input
     - Strange input
2. Define the expected results
3. Write test code

## Higher level testing
At higher level testing can be:
- Big picture understanding: Are you a person who understands what the software is really about? Can you prioritize test cases properly?
- Knowing how the pieces fit togheter: Do you understand how software works, and how it might fit into a greater ecosystem?
- Organization: Do you approach the problem in a structured manner or do you just spiut off anything that comes to your head? A good candidate will break down the parts into categories and this also help you to do a more thorough job creating the test cases.
- Practicality: Can you actually create reasonable testing plans? Your testing plans need to be realistic and feasible for a company to implement.

## Real world object
How would test a pen? or another real world object?

1. Who will use it? And why?

You need to discuss with your interviewer who is using the product and for what purpose. The answer may not be what you think.

2. What are the use cases?

3. What are the bounds of use?

The bounds of use might mean holding up to thirty sheets of paper without damage. Other examples enviromental like warm, cold, etc..

4. What are the stress / failure conditions?

A good discussion to have is about when it's acceptable (or even necessary) for the product to fail, and what failure should mean.

5. How would you perform the testing?
