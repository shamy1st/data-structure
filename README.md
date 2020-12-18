# Data Structure

* [Big O Notation](https://github.com/shamy1st/data-structure-big-o)

Linear Data-Structure
1. [Array](https://github.com/shamy1st/data-structure-array)
2. [Linked List](https://github.com/shamy1st/data-structure-linkedlist)
3. [Stack](https://github.com/shamy1st/data-structure-stack)
4. [Queue](https://github.com/shamy1st/data-structure-queue)
5. [Hashing](https://github.com/shamy1st/data-structure-hashing)

Non-Linear Data-Structure
6. [Binary Tree](https://github.com/shamy1st/data-structure-binary-tree)
7. [Binary Search Tree](https://github.com/shamy1st/data-structure-binary-search-tree)
8. [AVL Tree](https://github.com/shamy1st/data-structure-avl-tree)
9. [Heap](https://github.com/shamy1st/data-structure-heap)
10. [Trie](https://github.com/shamy1st/data-structure-trie)
11. [Graph](https://github.com/shamy1st/data-structure-graph)
12. [Undirected Graph](https://github.com/shamy1st/data-structure-undirected-graph)

Advanced
13. Advanced Lists
14. Matrix
15. Misc
16. Red-Black Tree
17. B-Tree
18. Splay Tree
19. 2-3 Tree
20. Segment Tree
21. Binary Indexed Tree
22. Suffix Array
23. Suffix Tree
24. K Dimensional Tree

### Cheatsheet

average/worst      |        indexing     | search              | add                 | remove(index or value)
-------------------|---------------------|---------------------|---------------------|-----------------------
Basic Array        | O(1)                | O(n)                | -                   | -
Dynamic Array      | O(1)                | O(n)                | O(n)                | O(n)
Singly Linked List | O(n)                | O(n)                | O(1)                | O(n)
Doubly Linked List | O(n)                | O(n)                | O(1)                | O(n)
Binary Search Tree | O(log n)/O(n)       | O(log n)/O(n)       | O(log n)/O(n)       | O(log n)/O(n)
AVL Tree           | O(log n)/O(log n)   | O(log n)/O(log n)   | O(log n)/O(log n)   | O(log n)/O(log n)
Trie               | -                   | O(L)                | O(L)                | O(L)

--                 | addFirst | addMiddle | addLast | removeFirst | removeMiddle | removeLast
-------------------|----------|-----------|---------|-------------|--------------|-----------
Singly Linked List | O(1)     | O(n)      | O(1)    | O(1)        | O(n)         | O(n)
Doubly Linked List | O(1)     | O(n)      | O(1)    | O(1)        | O(n)         | O(1)

--    | push | pop | peek | isEmpty
------|------|-----|------|--------
Stack | O(1) | O(1)| O(1) | O(1)

--                    | enqueue     | dequeue     | peek | isEmpty | isFull
----------------------|-------------|-------------|------|---------|-------
Queue                 | O(1)        | O(1)        | O(1) | O(1)    | O(1)
PriorityQueue (Array) | O(n)        | O(1)        | O(1) | O(1)    | O(1)
PriorityQueue (Heap)  | O(log n)    | O(log n)    | O(1) | O(1)    | O(1)

--  | put | remove | get | containsKey | containsValue
----|-----|--------|-----|-------------|--------------
Map | O(1)| O(1)   | O(1)| O(1)        | O(n)

average/worst    | addEdge   | removeEdge | queryEdge | findNeighbors | addNode       | removeNode    | space
-----------------|-----------|------------|-----------|---------------|---------------|---------------|----------------
Adjacency Matrix | O(1)/O(1) | O(1)/O(1)  | O(1)/O(1) | O(V)/O(V)     | O(V^2)/O(V^2) | O(V^2)/O(V^2) | O(V^2)/O(V^2)
Adjacency List   | O(K)/O(V) | O(K)/O(V)  | O(K)/O(V) | O(K)/O(V)     | O(1)/O(1)     | O(V^2)/O(V^2) | O(V + E)/O(V^2)
