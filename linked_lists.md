# Linked Lists
- a linked list is really just a head node which points to the next node
- delete a node n is setting the node before to point to the node after (just skip it)
    - can also delete a curr node without a previous pointer, but copying the next nodes data into the current one
- be aware of the null pointer and be aware of the head pointer
- linked list offer easy modification, but don't have random access (can't access any element in the list easily)
- Runner technique
    - two pointers, where one is ahead of the other, either by a fixed amount of by actually moving faster
    - ex. determine midpoint of a linked list.  Have two pointers, one moves by 1 node each time, the other by 2.  When the fast pointer reaches the end, the slow one will have reached the middle