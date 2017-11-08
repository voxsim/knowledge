## Testability
What the codes does is irrelevant; how the code is structured is all that matters for testability.

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

- https://martinfowler.com/bliki/ObjectMother.html
- https://martinfowler.com/bliki/SpecificationByExample.html
- https://martinfowler.com/bliki/SelfTestingCode.html
- https://martinfowler.com/bliki/TestDrivenDevelopment.html
- https://martinfowler.com/bliki/TestInvariant.html
- http://blog.cleancoder.com/uncle-bob/2017/05/05/TestDefinitions.html
- http://xunitpatterns.com/Fragile%20Test.html
- http://xunitpatterns.com/Obscure%20Test.html
- http://xunitpatterns.com/Slow%20Tests.html
- https://martinfowler.com/articles/microservice-testing/
- https://martinfowler.com/articles/nonDeterminism.html
- https://martinfowler.com/articles/mocksArentStubs.html
- https://martinfowler.com/articles/modernMockingTools.html
- https://martinfowler.com/articles/rise-test-impact-analysis.html
- https://martinfowler.com/articles/qa-in-production.html
- https://martinfowler.com/bliki/AssertionFreeTesting.html
- https://martinfowler.com/bliki/DatabaseAndBuildTime.html
- https://martinfowler.com/bliki/ClockWrapper.html
- https://martinfowler.com/bliki/ErraticTestFailure.html
- https://martinfowler.com/bliki/InMemoryTestDatabase.html
- https://martinfowler.com/bliki/Detestable.html
- https://martinfowler.com/bliki/GivenWhenThen.html
- https://martinfowler.com/bliki/MakingStubs.html
- https://martinfowler.com/bliki/JunitNewInstance.html
- https://martinfowler.com/bliki/ObjectMother.html
- https://martinfowler.com/bliki/SelfInitializingFake.html
- https://martinfowler.com/bliki/SpecificationByExample.html
- https://martinfowler.com/bliki/NashvilleProject.html
- https://martinfowler.com/bliki/SyntheticMonitoring.html
- https://martinfowler.com/bliki/TestCoverage.html
- https://martinfowler.com/bliki/SelfTestingCode.html
- https://martinfowler.com/bliki/TestDrivenDevelopment.html
- https://martinfowler.com/bliki/TestPyramid.html
- https://martinfowler.com/bliki/StaticSubstitution.html
- https://martinfowler.com/bliki/TestingResourcePools.html
- https://martinfowler.com/bliki/TestCancer.html
- https://martinfowler.com/bliki/TestDouble.html
- https://martinfowler.com/bliki/TestInvariant.html
- https://martinfowler.com/bliki/TestingLanguage.html
- https://martinfowler.com/bliki/Xunit.html
- https://stackoverflow.com/questions/4904096/whats-the-difference-between-unit-functional-acceptance-and-integration-test/4904533#4904533
- https://martinfowler.com/bliki/UnitTest.html
- https://stackoverflow.com/questions/333682/unit-testing-anti-patterns-catalogue
- https://www.youtube.com/watch?v=RlfLCWKxHJ0
- https://stanislaw.github.io/2016/01/25/notes-on-test-driven-development-by-example-by-kent-beck.html
- https://dev.to/barryosull/notes-from-growing-object-orientated-software-guided-by-tests
- http://wiki.c2.com/?TestDrivenDevelopment
- [ Writing Good Tests - Matteo Baglini - #iad14 ](https://vimeo.com/115568045)
