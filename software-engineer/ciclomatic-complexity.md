# Cyclomatic complexity

Cyclomatic complexity is a measure of source code complexity that has been correlated to number of coding errors in several studies. It is calculated by producing a ControlFlowGraph of the code, and then counting:

* E = number of edges in the graph.
* N = number of nodes in the graph.
* P = number of nodes that are exit points (last instruction, return, exit, etc.)

Then cyclomatic complexity = E - N + P

The metric tries to capture the number of paths through the code, and thus the number of required test cases. It is widely used, but has been criticized for not capturing the additional complexity implied in nested control structures.
