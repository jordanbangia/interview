# [Trees](https://www.wikiwand.com/en/Tree_(data_structure))
- a tree is defined as a node (the root) which holds some value, together with references to other nodes
    - this also defines a directed graph, so extra conditions are added:
        - at most 1 reference can point to any given node (a node can only have 1 parent)
        - no node in the tree points to the root
- as such, a tree is just a special case of directed graph
    - the graph definition: a connected (directed in this context) graph with no cycles
- binary trees (branching factor=2) are recusrivley built from nodes that have pointers to the left and right child
- binary trees aren't necessarily binary search trees (BSTs) which require that the left children are less than or equal to the current node which is less than all the right nodes
- a balanced tree has approximatley all nodes filled in at all levels (i.e. doesn't go super deep on the left side with only few elements on the right).  This makes it faster to search
- depth and height
    - a node's depth = the number of edges from the node to the trees root node.  A root node has depth = 0
    - a node's height = the number of edges on the longest path from the node to the leaf.  Leaf node will have a height of 0
    - the depth and height of a *tree* are equal
- full and complete is a tree where leaves are at the bottom and each non-leaf node has exactly children
    - full = every node other than the leaves has 2 children.  i.e. every node has iether 0 or 2 children
    - complete = every level (except the last) is completely filled and all nodes are as far left as possible. i.e. as compact as possilbe
    - in a perfect tree, heigh h = O(logn)
- Depth First Traversal (DFS) prefixes are in reference to when the root/current node is visited
    - pre-order traversal means first the root, then the left children, then the right children
    - post-order traversal means first the left, then the right, then the root
    - both can be done using recursion
- Breadth First Traversal (BFS) goes through nodes from top to bottom, going through an entire level first
- In order succesor
    - important in a lot of binary tree operations
    - the next node in in-order traversal, i.e. the node with the smallest key that's still greater than the current node's key

### Heaps
- a natural implementation of the priority queue
    - the highest priority element (whether min or max) recursivley sits at the top of the heap
    - works by maintaing a partial ordering, so less expensive than fully sorted, but more valualbe than no ordering
- a complete tree where the highest (or lowest) priority element is always stored at the root - hence a heap
- a max heap is one whre the node is always greater than or equal to its children, a min heap is one where the node is always lesser than or equal to its children
- these are used to implement priority queues and to do heap sort
- there is no implied ordering within a level (no ordering between siblings), so a heap is not a sorted structure
- insertion and deletion (get max/min element) are both O(logN) where N is the number of nodes
- Binary Heaps are implemented in arrays
    - note that any binary tree can be implemented in an array
    - makes extra sense for heaps though because heaps are guaranteed to be complete trees, thus the implementation is compact
    - if a non-complete tree is implemented in an array, thn there may be empty slots because a node may only have 1 child
    - saves space because can use array position to implicitly maintain the ordering property instead of storing pointers
- For the array implementations
    - let n be the number of elements in the heap, and i be an arbitrary index
    - the tree root is at index 0, valid indices 0 through n-1, then each element at index i has;
        - children at indices 2i+1 and 2i+2
        - it parent at floor((i-2)/2)
    - if the treet root is at index 1, valid indices 1 through n, each element at index i:
        - children at indices 2i and 2i+1
        - parent at floor(i/2)

#### Heap Operations
- both insert and remove
    - remove only removes the root since that's all that is needed
    - both operations operate on the ends of the heap (beginning or end)
    - after the operation, the ordering is modified by traversing the heap
        - insert performs up-heap/sift-up
        - removal performs a down-heap/sift-down
        - both operations are O(logN)
- up-heap/shift-up is used to restore heap ordering when a new element is added to the end
    - compare added element with is parent, if they are in the correct order, stop
    - if not, swap with its parent and repeat
- down-heap/shift-down is used to restore the heap ordering when the root is delete and replaced with the last element
    - compare the new root with its children, if they are in the correct order stop
    - if not, swap the element with one of its children adn return to the previous step
        - swap with the smaller child in min-heap and larger child in max-heap
        - boils down to swapping with higher priority
- heapify - given a complete binary tree, turn the structure into a heap
    - we want the heap property to be obtained, so we need to ensure that each parent node is greater (or less) than its children
    - starting at the last parent node (take the last node and get its parent through index arithmetic), call down-heap on it
    - repeat this process for all other parent nodes
- heapsort just entails copying elements to be sorted into an array, heapifying it, then taking the max (root) out each time and putting it at the end of the result array
    - this can be done in-placae where one section is for the heap and the other is for the sorted list
    - each iteration of the algorithm will reduce the heap by 1 and increase the sorted list by 1
    - heapsort is similar to insertion sort in that each step of the algorithm takes the max element from the unsorted section and moves it to the sorted section
- note that a heap is ***not*** a binary search tree, so we can't efficiently find a given key using binary search

### Self-Balancing Binary Trees
- binary trees have performance proportional to their height, so keeping the height small maximizes performance
- in the owrse case, a treee approximates a linked list; a maximally unbalanced tree is just a linked list where the height is 1 less than the number of nodes
- a balanced tree has performance O(log n)
- self balancing trees thus guarantee balanced-ness and consequently efficient performance

#### [Red-Black Trees](http://www.eternallyconfuzzled.com/tuts/datastructures/jsw_tut_rbtree.aspx)

![Red Black Tree](/images/red_black_tree.png)

- guarantees searching, insertion, and deletion in O(log n)
- each node has a color associated with it, red or black
    - how the tree is painted ensures the balance
    - when modified, the tree is re-arranged and re-painted to keep necessary color properties
- originally an abstraction of symmetric binary B-trees, also called 2-3-4 or 2-4 trees
    - red-black trees are really isomorphic to 2-4 trees, they are equivalent data structures
    - [Good](https://www.cs.princeton.edu/~rs/AlgsDS07/09BalancedTrees.pdf) [links](https://www.wikiwand.com/en/2%E2%80%933%E2%80%934_tree)
    - in a 2-4 tree, there a 3 kinds of nodes
        - 2-node: 1 key and (if internal) 2 children
        - 3-node: 2 keys and 3 children
        - 4-node: 3 keys and 4 children
    - all leaves are at the same depth, the bottom level. So every path from root to leaf is the same length, ensuring perfect balance
- red-black trees have the following properties:
    1.    every node is either red or black
    2. all leave nodes are black
        - leves can either be an explicit node with no data or just NIL nodes
    3. if a node is red, both its children are black
    4. every path from a given node n to a descendant leaf has the same number of black nodes (not count node n)
        - we call this number the black height of n, which is denoted as bh(n)
- these explicit properties give rise to this critical property: the path from the root to the farthest leaf node is no more than twice as long as the path from the root to the nearest leaf, ensuring that the tree is roughly height-balanced
- this limits the heigh of any red-black tree, ensuring that even in the worst case, search, insert, and deletion are still efficient
- the balance property is guaranteed throught he combination of properties 3 and 4
    - for a red-black tree T, let B be the number of black nodes in property 4 (since every path has the same number of black nodes)
    - let the shortest possible path from the root of T to any leaf consist of B black nodes
    - longer possible paths may be constructed by inserting red nodes
    - however, property 3 makes it impossible to insert more than 1 consecutive red node
    - therefore, ignoring any black NIL leaves, the longest possible path consists of 2*B nodes, alternating black and red (this is the worst case)
    - the shortest possible path has all black nodes, and the longest possible path alternates between red and black nodes
    - since all maximal paths have the same number of black nodes, by property 4, this shows that no path is more than twice as long as any other path
- a red-black tree can be converted to a 2-4 tree by remembering that red nodes are part of a logical 2-4 B-tree node ("horizontally" linked within the 2-4 node), and black nodes separate the logical 2-4 nodes with normal vertical links
    - so, to convert a red-black tree to a 2-4 form, just move the red nodes up so that they become horizontally linked with their parent black node to form a logical 2-4 node
    - all leaf nodes will be at the same depth
    - [example](https://www.wikiwand.com/en/Red%E2%80%93black_tree)
- search and other read-only operations are the same as those used to BST
- insertion and deletion are much more complex, because they may violate red-black properties and then must be fixed with color changes and rotations
    - in practice these are quite quick, color changes are ~ O(1)
    - a tree rotation is a binary tree operation that changes the structure wihtout affecting the order of the elements.  That is: in order traversal is the same pre- and post- rotation
    - [read more](https://www.wikiwand.com/en/Tree_rotation)
    - essentially, a right rotation (the root moves right) on a root node X has X become the right child of the new root, which will be X's former left child
    - order in the descendants is maintained through realizing that the right child of a left child of a root node can become the left child of the root without violating any binary tree constraints

#### [AVL Trees](https://www.wikiwand.com/en/AVL_tree)
- more rigidly balanced than red-black trees, leading to slower insertion and removal, but faster search, so better for read-heavy use cases
- critical property: the heights of the two child subtrees of any node differ by at most one; if at any time they differ by more than one, rebalancing (with tree rotations) is done to restore this property
- retrieval, insertion, and deletion, as with red-black trees, are O(log n) in the worst case

### Trie
![](/images/trie.png)
- a trie (or radix tree or prefix tree) is a n-ary tree variant in which characters are stored at each node, such that each path down the tree may represent a word
    - unlike a binary search tree, no node in the tree stores the key associated with that node; instead, its position in the tree defines the key with which it is associated
    - all the descendants of a node have a common prefix of the string associated with that node, and the root is associated with the empty string
    - note that tries do not have to be keyed by character strings; other ordered lists can work too
        - ex. permutations on a list of digits


### Misc.
[Pretty good overall reference](https://www.cs.cmu.edu/~adamchik/15-121/lectures/Trees/trees.html)