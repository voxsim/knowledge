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
