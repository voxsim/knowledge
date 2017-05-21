# Big-O Notation
Big-O Notation is a way of roughly measuring the performance of algorithms
in order to compare one against another when discussing them.

Big-O is a mathematical notation that we borrowed in computer science to
classify algorithms by how they respond to the number (N) of items that you
give them.

There are two primary things that you measure with Big-O:

-*Time complexity** refers to the total count of operations an algorithm
  will perform given a set of items.

-*Space complexity** refers to the total memory an algorithm will take up
  while running given a set of items.

We measure these independently from one another because while an algorithm
may perform less operations than another, it may also take up way more
memory. Depending on what your requirements are, one may be a better choice
than the other.

These are some common Big-O's:

|Name         | Notation    |How you feel when they show up at your party
|-------------|-------------|-------------------------------------------
|Constant     | O(1)        |AWESOME!!
|Logarithmic  | O(log N)    |GREAT!
|Linear       | O(N)        |OKAY.
|Linearithmic | O(N log N)  |UGH...
|Polynomial   | O(N ^ 2)    |SHITTY
|Exponential  | O(2 ^ N)    |HORRIBLE
|Factorial    | O(N!)       |WTF

To give you an idea of how many operations we're talking about. Let's look
at what these would equal given the (N) number of items.

           N = 5            10             20             30
-----------------------------------------------------------------------
O(1)           1            1              1              1
O(log N)       2.3219...    3.3219...      4.3219...      4.9068...
O(N)           5            10             20             30
O(N log N)     11.609...    33.219...      84.638...      147.204...
O(N ^ 2)       25           100            400            900
O(2 ^ N)       32           1024           1,048,576      1,073,741,824
O(N!)          120          3,628,800      2,432,902,0... 265,252,859,812,191,058,636,308,480,000,000

As you can see, even for relatively small sets of data you could do alot*
of extra work.

With data structures, you can perform 4 primary types of actions:
Accessing, Searching, Inserting, and Deleting.

It is important to note that data structures may be good at one action but
bad at another.

                           Accessing    Searching    Inserting    Deleting
   -------------------------------------------------------------------------
                 Array     O(1)         O(N)         O(N)         O(N)
           Linked List     O(N)         O(N)         O(1)         O(1)
    Binary Search Tree     O(log N)     O(log N)     O(log N)     O(log N)

Or rather...

                           Accessing    Searching    Inserting    Deleting
   -------------------------------------------------------------------------
                 Array     AWESOME!!    OKAY         OKAY         OKAY
           Linked List     OKAY         OKAY         AWESOME!!    AWESOME!!
    Binary Search Tree     GREAT!       GREAT!       GREAT!       GREAT!

Even further, some actions will have a different "average" performance and a
"worst case scenario" performance.

There is no perfect data structure, and you choose one over another based on
the data that you are working with and the things you are going to do with
it. This is why it is important to know a number of different common data
structures so that you can choose from them.

In detail:

Data structure|Time Complexity Average Access|Time Complexity Average Search|Time Complexity Average Insert|Time Complexity Average Delete|Time Complexity Worst Access|Time Complexity Worst Search|Time Complexity Worst Insert|Time Complexity Worst Delete|Space Complexity (Worst)|
--------------|------------|------------|--------|--------|-----------|-----------|-------|-------|----|
Array         |Θ(1)        |Θ(n)        |Θ(n)    |Θ(n)    |O(1)       |O(n)       |O(n)   |O(n)   |O(n)|
Stack|Θ(n)|Θ(n)|Θ(1)|Θ(1)|O(n)|O(n)|O(1)|O(1)|O(n)|
Queue|Θ(n)|Θ(n)|Θ(1)|Θ(1)|O(n)|O(n)|O(1)|O(1)|O(n)|
Singly-Linked List|Θ(n)|Θ(n)|Θ(1)|Θ(1)|O(n)|O(n)|O(1)|O(1)|O(n)|
Doubly-Linked List|Θ(n)|Θ(n)|Θ(1)|Θ(1)|O(n)|O(n)|O(1)|O(1)|O(n)|
Skip List|Θ(log(n))|Θ(log(n))|Θ(log(n))|Θ(log(n))|O(n)|O(n)|O(n)|O(n)|O(n log(n))|
Hash Table|N/A|Θ(1)|Θ(1)|Θ(1)|N/A|O(n)|O(n)|O(n)|O(n)|
Binary Search Tree|Θ(log(n))|Θ(log(n))|Θ(log(n))|Θ(log(n))|O(n)|O(n)|O(n)|O(n)|O(n)|
Cartesian Tree|N/A|Θ(log(n))|Θ(log(n))|Θ(log(n))|N/A|O(n)|O(n)|O(n)|O(n)|
B-Tree|Θ(log(n))|Θ(log(n))|Θ(log(n))|Θ(log(n))|O(log(n))|O(log(n))|O(log(n))|O(log(n))|O(n)|
Red-Black Tree|Θ(log(n))|Θ(log(n))|Θ(log(n))|Θ(log(n))|O(log(n))|O(log(n))|O(log(n))|O(log(n))|O(n)|
Splay Tree|N/A|Θ(log(n))|Θ(log(n))|Θ(log(n))|N/A|O(log(n))|O(log(n))|O(log(n))|O(n)|
AVL Tree|Θ(log(n))|Θ(log(n))|Θ(log(n))|Θ(log(n))|O(log(n))|O(log(n))|O(log(n))|O(log(n))|O(n)|
KD Tree|Θ(log(n))|Θ(log(n))|Θ(log(n))|Θ(log(n))|O(n)|O(n)|O(n)|O(n)|O(n)|
