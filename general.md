# General

## Try and do this for every question:
- repeat the problem out loud (slowly but confidently)
- ask questions, check assupmtions, know what the constraints are
- write these all down
- talk about the problem out loud
- if difficult, start working out examples
- start with a **naive** brute force solution
- check for edge cases, null conditions, empty conditions
- run through the algorithm by hand, check state at each step
- know the time space complexity [here](complexity.md)


## Heuristics / General Tips
- always consider *hash tables/dictionaries*
    - O(1) access time, very common way to go from brute force to a better solution
    - often creates a trade off in terms of time and space
- if the question seems *array* related, try *sorting* first
- if *search* related, consider using a *binary search* or some variant of *trees*
- start with a **brute force** solution, then look for repeated work that can be modified out
- two pointer trick: move one pointer twice as fast as another.  can be used to find the midpoint or loops in a linked list
- two pointer trick: start one at the beginning and one at the end of a list.  Can detect palindromes and sum a list in half the time
- if the problem requires parsing a tree or graph traversal/reversal, consider using a stack
- recursion/dynamic programming - does solving the problem for size N-1 make solving for N easier?  then do dynamic or recursion
    - careful though, it can hard on time complexity
- a lot of problems can be turned into graph problems and/or use breadth-first/depth-first search
- if dealing with a lot of strings, try using a prefix tree/trie
- any time you repeadetly are taking the min or max of a dynamic collection, think heaps
    - if you don't need to insert random elements, prefer a sorted array

#### Space Time Trade Off
- to create a better run time, try storing data
- i.e. do a single pass of an array (O(N) time) and store in a hashtable (O(N) space) instead of doing multiple passes and saving nothing(O(N^2) time and O(1) space).
- try to think of what information could be stored to make life easier
- another example:  max stack where each element contains both the value and the max of everything below it in the stack

#### Greedy Solutions
- iterate through the problem space, taking the optimal solution "so far" until the end
- works if the problem has "optimal substructure", which means stitching together optimal solutions to subproblems yields an optimal solution

 