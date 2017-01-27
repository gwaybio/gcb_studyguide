# Computational Complexity

Asymptotic bounds on how long to expect an algorithm to identify an answer.
Also refers to how much memory is required.

**Important:** An algorithm has complexity, not a problem. A problem is only
assigned a complexity based on the current algorithm to solve it, but there
is no guarantee that the solution is optimal.

## P Class Algorithms

P, or "Polynomial", means that the solution is tractable, or, that the solution
is expected to return in a finite state of time. Some big "O" notation examples
include *O(n)* and *O(n^2)*.

## EXP Class Algorithms

Polynomial function to the power of n. E.g. *O(2^n)*. The problem can be solved
with conventional means. Often times has a solution that can be checked in P
time.

## NP Class Algorithms
NP, or "Non-deterministic Polynomial", means that the algorithm can be checked
in Polynomial time if the solution exists, but it is not clear that any
solution exists.
