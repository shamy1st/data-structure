# Data Structure

* [Big O Notation](https://github.com/shamy1st/data-structure-big-o)

Linear Data-Structure
* [Array](https://github.com/shamy1st/data-structure-array)
* [Linked List](https://github.com/shamy1st/data-structure-linkedlist)
* [Stack](https://github.com/shamy1st/data-structure-stack)
* [Queue](https://github.com/shamy1st/data-structure-queue)
* [Hashing](https://github.com/shamy1st/data-structure-hashing)

Non-Linear Data-Structure
* [Binary Tree](https://github.com/shamy1st/data-structure-binary-tree)
* [Binary Search Tree](https://github.com/shamy1st/data-structure-binary-search-tree)
* [AVL Tree](https://github.com/shamy1st/data-structure-avl-tree)
* [Heap](https://github.com/shamy1st/data-structure-heap)
* [Trie](https://github.com/shamy1st/data-structure-trie)
* [Graph](https://github.com/shamy1st/data-structure-graph)
* [Undirected Graph](https://github.com/shamy1st/data-structure-undirected-graph)

Advanced
* Advanced Lists
* Matrix
* Misc
* Red-Black Tree
* B-Tree
* Splay Tree
* 2-3 Tree
* Segment Tree
* Binary Indexed Tree
* Suffix Array
* Suffix Tree
* K Dimensional Tree

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
