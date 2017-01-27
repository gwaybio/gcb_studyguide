# String Matching

## Considerations

- Size of genomics problems are typically very large
  - Large storage requirements
  - Large run-time requirements
    - Time and storage depend on processing speed, bandwidth, parallelization,
    reading and writing executions, etc.
 - Must consider [computational complexity](https://en.wikipedia.org/wiki/Computational_complexity_theory)
 and [Big O notation](https://justin.abrah.ms/computer-science/big-o-notation-explained.html)

## Classes of String Matching

### Exact Search

All elements of any string `P` must match all corresponding elements of `S`
starting at some offset `k` of `S`. Consider the language to be DNA nucleotides
`{A, C, T, G}`.

- Naive Search
  - Compare all elements of P to all possible substrings of S
    - `O(nm)` complexity if `len(P) = n` and `len(S) = m`
  - Many ways to make this less complex
    - Stop searching in `P` if mismatch found
    - Offset more than +1 depending on extent of mismatch
    - Generate offset tables or suffix trees of `P` without looking at `S`
      - This will inform how to move the offset without requiring computation
      but does require storage
- [Boyer Moore Algorithm](http://www-igm.univ-mlv.fr/~lecroq/string/node14.html)
  - State of the art for exact string matching
    - Best Complexity `O(n/m)` (gets smaller with bigger search spaces)
    - Worst case `O(nm)` but can be reduced to `O(n)`
  - Essentially, move P from left to right across S but compare starting at
  rightmost match
  - Store a "bad character table" and "suffix match table" to describe how to
  move the offset when a mismatch happens.
    - *bad character table* defines how to move the offset based on which type
    of mismatch is observed
    - *suffix match table* builds suffix pattern matches from `P` and is
    dictated by substring patterns in `P`.
    - Move offset `max(c(bad_character, suffix_tree))`
  - Works well when the alphabet is large and complex
    - DNA nucleotide language is not large so it can be improved

### Inexact Search

Searching through a database for any string `P` allowing for `k` number of
mismatches

- Suffix Trees and Tries (pronounced "trys")
  - [Slides by Ben Langmead reviewing them](http://www.cs.jhu.edu/~langmea/resources/lecture_notes/tries_and_suffix_tries.pdf)
  - Provides a lot of information
    - Location of substrings in the larger string
    - Starting positions of all elements in the string
    - How many of each element are there
  - Some drawback
    - Construction time is O(n^2)
    - Larger storage than original string O(n^2)
      - Big problem when database is large
  - Boyer Moore is preferable for smaller problems that are not done
  repetitively.
    - Only O(n) to construct
    - Searching is sub-linear O(n/m)
    - Storage only O(m)
- Suffix arrays
  - Form the basis of [Burrows-Wheeler Transform](https://en.wikipedia.org/wiki/Burrows%E2%80%93Wheeler_transform)
    - [Youtube description](https://www.youtube.com/watch?v=4n7NPk5lwbI)

### Finite State Automata

Different approach for string search problem - FSA have internal states and
read input. Based on these two items (current state and input) output will
happen. They are "memory-less" since they only depend on current state, but
they do require a transition table to operate. Can match a string based on
input passing through a series of states in order until reaching an accepting
state.
