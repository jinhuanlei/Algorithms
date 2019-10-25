## Algorithms and Data Structures
Implement the common algorithms and data structures and analysing its Time/ Space complexity. Always try to find the optimal solution.

### Algorithms
1. Binary Search

1. Tree
    1. Tree Traverse
    1. Binary Tree
    1. BST
1. Graph    
    1. Graph Traverse
        1. DFS
        1. BFS-1 (Breadth first search)
        1. BFS-2 (Best first search)
1. Recursion
    1. Math
    1. 1D or 2D array
        1. Eight queen or N queen
    1. Linked List
    1. String
    1. Tree
        1. Tricks
            * What do you expect from your lchild/rchild ?
            * What do you want to do in the current layer ?
            * What do you want to report to your parent ?
1. String
    1. Char Removal
        1. remove some particular chars from a string.
        1. remove all​ leading/trailing/duplicated​ empty spaces from a string.
    1. De-duplication
    1. SubString
        1. Optimal Solution
            * Rabin-Karp
            * KMP
    1. String Reversal
    1. String Replacement
    1. String Shuffling
    1. Permutation
    1. Encoding / Decoding
    1. Sliding Window
1. Bit Operations

    Can be solved by building blocks below

    * Get kth bit   =>   (x >> k) & 1
    * Set kth bit as 1  =>  x | (1 << k)
    * Set kth bit as 0  =>  x & (~(1 << k))
    
1. Dynamic Programming

和recursion相反, 把一个大问题通过比它小的问题来解决(类似数学归纳法)

* Solutions for 1D problems
    * Linear scan and look back
    * 左大段,右小段
        
    

#### Data structures
1. Linked List
1. Stack
1. Queue
1. Deque
1. Heap(PriorityQueue)
1. HashMap

#### Interview Steps - CART
1. Clarification
    1. Object
        * Null
        * Empty
    1. Collection / Array
        * Sorted
            * Ascending
            * Descending
        * Unsorted
        * Duplicate
        * Contains target or not(search element)
    1. String
        * Leading, trailing spaces
        * in place or not
        * Duplicate Elements
1. Assumption
1. Result
    1. Time Complexity
        * Collections (Use different symbol M N to  represent)
        * Graph Use V(Vertices) and E(Edge)
        * Tree we need to consider balance tree or not(Worst case become a Linked List)
1. Testing

