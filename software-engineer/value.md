# Value (Value Object)

Values are immutable instances that model fixed quantities. They have no in- dividual identity, so two value instances are effectively the same if they have the same state. This means that it makes no sense to compare the identity of two values; doing so can cause some subtle bugs—think of the different ways of comparing two copies of new Integer(999). That’s why we’re taught to use string1.equals(string2) in Java rather than string1 == string2.
