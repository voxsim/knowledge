# Connascence
Connascence is a software quality metric & a taxonomy for different types of coupling.

## Subject to Change
All code is subject to change. As the real world changes, so too must our code. Connascence gives us an insight into the long-term impact our code will have on flexibility, as we write it. Maintaining a flexible codebase is essential for maintaining long-term development velocity.

## A Flexible Metric
Connascence is a metric, and like all metrics is an imperfect measure. However, connascence takes a more holistic approach, where each instance of connascence in a codebase must be considered on three separate axes:
* Strength. Stronger connascences are harder to discover, or harder to refactor.
* Degree. An entity that is connascant with thousands of other entities is likely to be a larger issue than one that is connascant with only a few.
* Locality. Connascant elements that are close together in a codebase are better than ones that are far apart.

The three properties of Strength, Degree, and Locality give the programmer all the tools they need in order to make informed decisions about when they will permit certain types of coupling, and when the code ought to be refactored.

## A Vocabulary for Coupling
Arguably one of the most important benefits of connascence is that it gives developers a vocabulary to talk about different types of coupling. Connascence codifies what many experienced engineers have learned by trial and error: Having a common set of nouns to refer to different types of coupling allows us to share that experience more easily.

# Properties
## Strength
The strength of a form of connascence is determined by the ease with which that type of coupling can be refactored. For example, connascence of name is a weak form of connascence because renaming entities across a codebase is usually reasonably trivial. However, connascence of meaning is considered a stronger form of connascence since semantic meaning is harder to find across an entire codebase.

Static connascences are considered to be weaker than dynamic connascences, since static connascences can be determined simply by examining the source code. Dynamic connascences require knowledge of run-time behavior, and thus are harder to reason about.

Strength and locality should be considered together. Stronger forms of connascence are often found within the same function, class, or module where their impact can be more easily observed.

## Locality
The locality of an instance of connascence is how close the two entities are to each other. Code that is close together (in the same module, class, or function) should typically have more, and higher forms of connascence than code that is far apart (in separate modules, or even codebases). Many of the stronger forms of connascence that can be devastating to the readability and maintainability of a codebase when they appear far apart are innocuous when close together.
Locality matters! Stronger connascences are more acceptible within a module. Weaker connascences should be used between entities that are far apart (in separate modules or even codebases).

## Degree
The degree of a piece of connascence is related to the size of its impact. Does the coupling in question affect 2 entities, or 200?

# Type of Connascence

## Connascence of Name
Connascence of name is when multiple components must agree on the name of an entity. Method names are an example of this form of connascence: if the name of a method changes, callers of that method must be changed to use the new name.

Almost any code example involves connascence of name. Consider the following class declaration taken from the Python standard library (method implementation has been omitted for clarity):

class Request:

```python
    def __init__(self, url, data=None, headers={},
                 origin_req_host=None, unverifiable=False,
                 method=None):
        pass

    def set_proxy(self, host, type):
        pass
```
Changing the name of any part of this code will cause code that uses this class to break, including:
- Changing the class name from Request.
- Changing any of the method names (such as set_proxy).
- Changing the name of any of the parameters to either __init__ or set_proxy.

Connascence of name is unavoidable, since we refer to entities using labels. If we change the name of an entity when we declare it, we must also change all code that refers to that entity. For this reason, connascence of name is the weakest connascence. However, it also illustrates how important it is to name entities in code well.

## Connascence of Type 
Connascence of type is when multiple components must agree on the type of an entity. In a statically typed language, these issues are often (but not always) caught by the compiler.

## Connascence of Meaning
Connascence of meaning is when multiple components must agree on the meaning of particular values. Consider some code that processes credit card payments. The following function might be used to determine if a given credit card number is valid or not:
```python
def is_credit_card_number_valid(card_number):
    # Check for 'test' credit card numbers:
    if card_number == "9999-9999-9999-9999":
        return True
    # Do normal validation:
    # ...
```
The problem here is that all parts of this system must agree that 9999-9999-9999-9999 is the test credit card number. If that value changes in one place, it must also change in another.

Here's another example where user roles are encoded as integers:
```python
def get_user_role(username):
    user = database.get_user_object_for_username(username)
    if user.is_admin:
        return 2
    elif user.is_manager:
        return 1
    else:
        return 0
```

Elsewhere, code might need to check that a given username is an administrator, like so:
```python
if get_user_role(username) != 2:
    raise PermissionDenied("You must be an administrator")
```

Connascence of meaning can be improved to connascence of name by moving the "magic values" to named constants, and referring to the constants instead of the values. However in doing so, we have increased the amount of connascence of name (since we now need a third location to store the constant).

Another common example of connascence of meaning is when None is used as a return value. This frequently occurs in functions that are tasked with finding an object. If that object isn't found, the function might return None.
```python
def find_user_in_database(username):
    return database.find_user(username=username) or None
```

However, the function might also return None in an error condition:
```python
def find_user_in_database(username):
    try:
        return database.find_user(username=username) or None
    except DatabaseError:
        return None
```
The problem in both these cases is that a semantic meaning is being assigned to the None value. If multiple different meanings are assigned to the same None value in the same codebase, the programmer must remember which meaning applies to which case. This can be improved to connascence of name by returning an explicit object that represents the case in question:
```python
def find_user_in_database(username):
    try:
        return database.find_user(username=username) or ObjectNotFound
    except DatabaseError:
        return None
```
We still have connascence of meaning in the error case, but at least the None value is no longer ambigous. The error case could also be improved to connascence of name in a similar way.

Another common example of connascence of meaning is when we use primative numeric types to represent more complex values. Consider this line of code in a codebase that processes payments:
```python
unit_cost = 49.95
```

What currency is that cost expressed in? US dollars? British pounds? How do you ensure that two costs with different currencies are not added together? Similar to the examples above, the problem is that a semantic meaning is being added to the primative type. It can be improved to connascence of type by creating a 'Cost' type that disallows operations between different currencies:
```python
unit_cost = Cost(49.95, 'USD')
```

This particular problem is often called *Primitive Obsession*, and can be generically described as using primitive data types to represent more complex domains.

## Connascence of Position
Connascence of position is when multiple entities must agree on the order of values. Connascence of position also frequently occurs in function argument lists.

## Connascence of Algorithm
Connascence of algorithm is when multiple components must agree on a particular algorithm.

# Type of Dynamic Connascence
## Connascence of Execution
Connascence of execution is when the order of execution of multiple components is important. Common examples include locking and unlocking resources, where locks must be acquired and released in the same order everywhere in the entire codebase.

Connascence of execution can also occur when using objects that encapsulate a state machine, and that state machine only allows certain operations in certain states. For example, consider a hypothetical EmailSender class that allows a caller to generate and send an email:
```python
email = Email()
email.setRecipient("foo@example.comp")
email.setSender("me@mydomain.com")
email.send()
email.setSubject("Hello World")
```
The last two lines show a trivial example of connascence of execution. The setSubject method cannot be called after the send method (at best it will do nothing). In this example the locality of the coupling is very low, but cases where the locality is very high can be much harder to find and fix (consider, for example a scenario where the last two lines are called on separate threads).

## Connascence of Timing
Connascence of timing is when the timing of the execution of multiple components is important.

## Connascence of Value
Connascence of value is when several values must change together. This frequently occurs between production code and test code. For example, consider an Article class, which represents a blog article. When it is instantiated, it is given some text contents, and its initial 'state' is 'draft':

```python
class ArticleState(Enum):
    Draft = 1
    Published = 2


class Article(object):

    def __init__(self, contents):
        self.contents = contents
        self.state = ArticleState.Draft

    def publish(self):
        # do whatever is required to publish the article.
        self.state = ArticleState.Published
```
Now imagine a hypothetical test that ensures that the publish method works:
```python
article = Article("Test Contents")
assert article.state == ArticleState.Draft
article.publish()
assert article.state == ArticleState.Published
```
The problem here is that the test requires knowledge of the initial state of the Article class: if the Article's initial state is ever changed, this test will break (this is arguably a bad test, since the first assertion has little to do with the intent of the test, but it's a common mistake). This code can be improved by adding an InitialState label to ArticleClass, and changing both the Article class and the test to refer to that label instead:
```python
class ArticleState(Enum):
    Draft = 1
    Published = 2
    InitialState = Draft


class Article(object):

    def __init__(self, contents):
        self.contents = contents
        self.state = ArticleState.InitialState
```
The test now becomes:
```python
article = Article("Test Contents")
assert article.state == ArticleState.InitialState
article.publish()
assert article.state == ArticleState.Published
```
Should we need to change the state machine of the Article class, we can do so by changing the ArticleState enumeration:
```python
class ArticleState(Enum):
    Preproduction = 1
    Draft = 2
    Published = 3
    InitialState = Preproduction
```
We have effectively introduced a level of indirection between the Article class and its initial state value.

## Connascence of Identity
Connascence of identity is when multiple components must reference the same entity.
