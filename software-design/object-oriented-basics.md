TBD

class, object (and the difference between the two)
instantiation
method (as opposed to, say, a C function)
virtual method, pure virtual method
class/static method
static/class initializer
constructor
destructor/finalizer
superclass or base class
subclass or derived class
inheritance
encapsulation
multiple inheritance (and give an example)
delegation/forwarding
composition/aggregation
abstract class
interface/protocol (and different from abstract class)
method overriding
method overloading (and difference from overriding)
polymorphism (without resorting to examples)
is-a versus has-a relationships (with examples)
method signatures (what's included in one)
method visibility (e.g. public/private/other)

For the OO-design weeder question, have them describe:

What classes they would define.
What methods go in each class (including signatures).
What the class constructors are responsible for.
What data structures the class will have to maintain.
Whether any Design Patterns are applicable to this problem.
Here are some examples:

Design a deck of cards that can be used for different card game applications.

Likely classes: a Deck, a Card, a Hand, a Board, and possibly Rank and Suit. Drill down on who's responsible for creating new Decks, where they get shuffled, how you deal cards, etc. Do you need a different instance for every card in a casino in Vegas?

Model the Animal kingdom as a class system, for use in a Virtual Zoo program.

Possible sub-issues: do they know the animal kingdom at all? (I.e. common sense.) What properties and methods do they immediately think are the most important? Do they use abstract classes and/or interfaces to represent shared stuff? How do they handle the multiple-inheritance problem posed by, say, a tomato (fruit or veggie?), a sponge (animal or plant?), or a mule (donkey or horse?)

Create a class design to represent a filesystem.

Do they even know what a filesystem is, and what services it provides? Likely classes: Filesystem, Directory, File, Permission. What's their relationship? How do you differentiate between text and binary files, or do you need to? What about executable files? How do they model a Directory containing many files? Do they use a data structure for it? Which one, and what performance tradeoffs does it have?

Design an OO representation to model HTML.

How do they represent tags and content? What about containment relationships? Bonus points if they know that this has already been done a bunch of times, e.g. with DOM. But they still have to describe it.

The following commonly-asked OO design interview questions are probably too involved to be good phone-screen weeders:

Design a parking garage.
Design a bank of elevators in a skyscraper.
Model the monorail system at Disney World.
Design a restaurant-reservation system.
Design a hotel room-reservation system.
A good OO design question can test coding, design, domain knowledge, OO principles, and so on. A good weeder question should probably just target whether they know when to use subtypes, attributes, and containment.
