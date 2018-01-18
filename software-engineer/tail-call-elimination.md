# Tail call elimination
Tail call is the last thing that a function does. Teoretically the compiler could figure out a tail call, so a function instead of returning itself can return the tail call. The elimination of that stack frame is tail call elimination.
It's really important in functional programming because we want to compose many function, but if we do not tail call elimination, this can cause the computer to crash do too many stackframes.
