# Information Hiding

The basic idea is that if code chunk A doesn't really need to know something about how code chunk B (which it calls) does its job, don't make it know it. Then, when that part of B changes, you don't have to go back and change A.

It is widely recognized as the most important criterion for judging the quality of a software design, although many more people think of it under a different name. The current phrase "if we do X we increase coupling between A and B". Increasing coupling is equivalent that breaking Information Hiding.
