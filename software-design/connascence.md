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

# Connascence of Name
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
