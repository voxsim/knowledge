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

## Kind of tests
- Acceptance / Scenario tests: test the whole system pretends to be an user
- Functional tests: test collection of classes as subsystems
- Integration tests: test the integration between your system and an external one
- Unit tests: test individual classes / methods in isolation

They are ordered from the bigger execution time to fewer, they are also ordered by scope frome huge to small.

## Test
It must be easier write the test and see test result and after writing the application. We should refactoring without have brittle tests and we should even delete the code and rewrite the application if we write the tests in a good way.
Every test should told us a story.
