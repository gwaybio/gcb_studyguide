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
 
 All elements of any string `P` must match all corresponding elements of `S` starting at some
 offset `k` of `S`. Consider the language to be DNA nucleotides `{A, C, T, G}`.
 
 - Naive Search
   - Compare all elements of P to all possible substrings of S
     - `O(nm)` complexity if `len(P) = n` and `len(S) = m`
   - Many ways to make this less complex
     - Stop searching in P if mismatch found
     - Offset more than +1 depending on extent of mismatch
     - Generate offset tables or suffix trees of P without looking at S
       - This will inform how to move the offset without requiring computation but does require
       storage
 - [Boyer Moore Algorithm](http://www-igm.univ-mlv.fr/~lecroq/string/node14.html)
   - State of the art for exact string matching
     - Best Complexity `O(n/m)` (gets smaller with bigger search spaces)
     - Worst case `O(nm)` but can be reduced to `O(n)`
   - Essentially, move P from left to right across S but compare starting at rightmost match
   - Store a "bad character table" and "suffix match table" to describe how to move the
   offset when a mismatch happens.
     - *bad character table* defines how to move the offset based on which type of mismatch is
     observed
     - *suffix match table* builds suffix pattern matches from `P` and is dictated by substring
     patterns in `P`.
     - Move offset `max(c(bad_character, suffix_tree))`
   - Works well when the alphabet is large and complex
     - DNA nucleotide language is not large so it can be improved
