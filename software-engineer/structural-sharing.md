# Structural sharing
In functional languages, every data is immutable by design. This can seems very slow for complex data, but this is can be healed using structural sharing: every time we do an action on a data, we recycle everything we can from the old data.

This opens a new class of data strctures called *persistent immutable data stractures*.
