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
