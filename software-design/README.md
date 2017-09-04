- http://connascence.io/
- https://cleancoders.com/videos
- https://martinfowler.com/bliki/
- https://github.com/xpeppers/starway-to-orione
- https://martinfowler.com/bliki/TestDouble.html
- https://martinfowler.com/bliki/IntegrationContractTest.html
- https://martinfowler.com/bliki/SelfInitializingFake.html
- https://martinfowler.com/articles/mocksArentStubs.html
- https://martinfowler.com/bliki/PageObject.html
- https://martinfowler.com/bliki/ObjectMother.html
- https://martinfowler.com/bliki/SpecificationByExample.html
- https://martinfowler.com/bliki/SelfTestingCode.html
- https://martinfowler.com/bliki/TestDrivenDevelopment.html
- https://martinfowler.com/bliki/TestInvariant.html
- https://martinfowler.com/bliki/IntegrationContractTest.html
- https://martinfowler.com/bliki/SelfInitializingFake.html
- http://xunitpatterns.com/Humble%20Object.html
- https://martinfowler.com/articles/continuousIntegration.html
- https://martinfowler.com/articles/feature-toggles.html
- https://martinfowler.com/articles/qa-in-production.html
- https://martinfowler.com/bliki/BlueGreenDeployment.html
- https://martinfowler.com/bliki/CanaryRelease.html
- https://martinfowler.com/bliki/CircuitBreaker.html
- https://martinfowler.com/bliki/ContinuousDelivery.html
- https://martinfowler.com/bliki/DevOpsCulture.html
- https://martinfowler.com/bliki/FeatureBranch.html
- https://martinfowler.com/bliki/DeploymentPipeline.html
- https://martinfowler.com/bliki/FeatureToggle.html
- https://martinfowler.com/bliki/PendingHead.html
- https://martinfowler.com/bliki/ReproducibleBuild.html
- https://martinfowler.com/bliki/ImmutableServer.html
- https://martinfowler.com/bliki/SemanticConflict.html
- https://martinfowler.com/bliki/InfrastructureAsCode.html
- https://martinfowler.com/bliki/PhoenixServer.html
- https://martinfowler.com/bliki/SyntheticMonitoring.html
- https://martinfowler.com/bliki/SnowflakeServer.html
- https://github.com/joebew42/study-path
- https://martinfowler.com/articles/designDead.html
- http://wiki.c2.com/?CouplingAndCohesion
- https://yurichev.com/blog/cyclomatic/
- https://martinfowler.com/tags/extreme%20programming.html
- https://martinfowler.com/tags/agile.html
- https://martinfowler.com/tags/design.html
- https://martinfowler.com/tags/evolutionary%20design.html
- https://robots.thoughtbot.com/avoid-the-threestate-boolean-problem
- https://ariya.io/2011/08/hall-of-api-shame-boolean-trap
- https://www.codeproject.com/articles/555855/introduction-to-cqrs
- https://cqrs.wordpress.com/documents/building-event-storage/
- https://github.com/flyeralarm/onboarding
- https://github.com/thoughtbot/guides/
- http://www.faqs.org/docs/artu/ch01s06.html
- http://courses.cs.washington.edu/courses/cse341/16sp/
- http://blog.cleancoder.com/uncle-bob/2017/05/05/TestDefinitions.html
- http://blog.wittchen.biz.pl/basic-code-refactoring-principles/
- https://tomassetti.me/oops-concepts/
- https://medium.com/javascript-scene/composing-software-an-introduction-27b72500d6ea
- https://www.youtube.com/watch?v=ElnqUIjLWVk
- http://www.faqs.org/docs/artu/ch01s06.html
- http://wiki.c2.com/?TechnicalDebt
- http://wiki.c2.com/?SeparationOfConcerns
- http://xunitpatterns.com/Fragile%20Test.html
- http://xunitpatterns.com/Obscure%20Test.html
- http://xunitpatterns.com/Slow%20Tests.html
- http://www.artima.com/weblogs/viewpost.jsp?thread=331531

Newly read:
- Practical Object Oriented Design in Ruby
- Extreme Programming Explained: Embrace Change
- Growing Object-Oriented Software, Guided by Tests
- Clean Code: A Handbook of Agile Software Craftsmanship
- Refactoring: Improving the Design of Existing Code
- Test Driven Development: By Example
- Refactoring to Patterns
- Implementing Domain-Driven Design
- The Agile Samurai: How Agile Masters Deliver Great Software
- Object Thinking


# Write shorter units of code

Shorter units (functions, in most languages) are easier to analyze, test, and reuse.

# Write simple units of code

Units with fewer decision points (conditional branches) are easier to analyze and test.

# Write code once

Duplication of code (including literals) should be avoided at all times, since changes will need to be made to each copy. Duplication is also a source of regression bugs.

# Keep unit interfaces small

Units with fewer parameters are easier to test and reuse

# TODO: write something about complexity (amount of state coder needs to keep in their head) per-unit and per-module

# Separate concerns in modules

Modules that are loosely coupled are easier to modify and evolve

# Couple architecture components loosely

Top-level business logic components that are more loosely coupled are easier to modify, and lead to a more modular system

# Keep architecture components balanced

A well balanced architecture, with not too many and not too few components, of uniform size, is the most modular and enables easy modification through separation of concerns.

# Keep your codebase small

A large system is difficult to maintain because more code needs to be analyzed, changed, and tested. Also, maintenance productivity _per line of code_ is lower in a large system than in a small system.

# write automated tests

# write clean code

1. leave no unit-level code smells behind
  1. long units
  2. branching units
  3. units /w large interfaces
2. leave no bad comments behind
3. leave no code in comments behind
4. leave no dead code behind
5. leave no long identifier names behind
6. leave no magic constants behind
7. leave no badly handled exceptions / error cases behind
