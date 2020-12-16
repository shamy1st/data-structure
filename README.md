# Data Structure

* [Big O Notation](https://github.com/shamy1st/data-structure#big-o-notation)
* [Array](https://github.com/shamy1st/data-structure#array)
* [Linked List](https://github.com/shamy1st/data-structure#linked-list)
* [Stack](https://github.com/shamy1st/data-structure#stack)
* [Queue](https://github.com/shamy1st/data-structure#queue)
* [Hashing](https://github.com/shamy1st/data-structure#hashing)
* [Binary Tree](https://github.com/shamy1st/data-structure#binary-tree)
* [Binary Search Tree](https://github.com/shamy1st/data-structure#binary-search-tree)
* [AVL Tree](https://github.com/shamy1st/data-structure#avl-tree)
* [Heap](https://github.com/shamy1st/data-structure#heap)
* [Trie](https://github.com/shamy1st/data-structure#trie)
* [Graph](https://github.com/shamy1st/data-structure#graph)
* [Undirected Graph](https://github.com/shamy1st/data-structure#undirected-graph)

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


### Big O Notation
![](https://github.com/shamy1st/data-structure/blob/main/images/big-o.png)

describe the performance (time or space) of an algorithm.
   * **O(1)**: constant (time or space).
   * **O(n)**: linear (time or space).
   * **O(n^2)**: quadratic (time or space).
   * **O(log n)**: logarithmic (time or space).
   * **O(2^n)**: exponential (time or space).

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

## Linear Data-Structure

### Array
![](https://github.com/shamy1st/data-structure/blob/main/images/array.png)

--                 | indexing | search | add    | remove(index or value)
-------------------|----------|--------|--------|-----------------------
Basic Array        | O(1)     | O(n)   | -      | -
Dynamic Array      | O(1)     | O(n)   | O(n)   | O(n)
    
        public class Main {
            public static void main(String[] args) {
                Array array = new Array(3);
                array.insert(10);
                array.insert(20);
                array.insert(30);
                array.insert(40);
                System.out.println(array.indexOf(40));
                array.removeAt(1);
                array.print();
            }
        }

        public class Array<T> {
            private T[] items;
            private int count;

            public Array(int length) {
                items = (T[]) new Object[length];
            }

            //O(n)
            public void insert(T item) {
                if(items.length == count) {
                    T[] temp = (T[]) new Object[items.length * 2];
                    for(int i=0;i<items.length;i++)
                        temp[i] = items[i];

                    items = temp;
                }
                items[count++] = item;
            }

            //O(n)
            public void removeAt(int index) {
                if(index < 0 || index >=count)
                    throw new ArrayIndexOutOfBoundsException();

                for(int i=index;i<count;i++)
                    items[i] = items[i+1];

                count--;
            }

            //O(n)
            public int indexOf(T item) {
                for(int i=0;i<count;i++)
                    if(items[i].equals(item))
                        return i;
                return -1;
            }

            public void print() {
                for(int i=0;i<count;i++)
                    System.out.println(items[i]);
            }
        }

### Linked List
![](https://github.com/shamy1st/data-structure/blob/main/images/linkedlist.png)

--                 | indexing | search | add    | remove(index or value)
-------------------|----------|--------|--------|-----------------------
Singly Linked List | O(n)     | O(n)   | O(1)   | O(n)
Doubly Linked List | O(n)     | O(n)   | O(1)   | O(n)

--                 | addFirst | addMiddle | addLast | removeFirst | removeMiddle | removeLast
-------------------|----------|-----------|---------|-------------|--------------|-----------
Singly Linked List | O(1)     | O(n)      | O(1)    | O(1)        | O(n)         | O(n)
Doubly Linked List | O(1)     | O(n)      | O(1)    | O(1)        | O(n)         | O(1)

![](https://github.com/shamy1st/data-structure/blob/main/images/singly-doubly-linkedlist.png)

        public class Main {
            public static void main(String[] args) {
                LinkedList<Integer> list = new LinkedList<>();
                list.addLast(10);
                list.addLast(20);
                list.addLast(30);
                list.removeLast();
                System.out.println(list.size());
            }
        }

        //Singly Linked List
        public class LinkedList<T> {
            private class Node<T> {
                private T value;
                private Node<T> next;

                public Node(T value) {
                    this.value = value;
                }
            }

            private Node<T> head;
            private Node<T> tail;
            private int size;

            private boolean isEmpty() {
                return head == null;
            }

            //O(1)
            public void addFirst(T item) {
                Node node = new Node(item);
                if(isEmpty())
                    head = tail = node;
                else {
                    node.next = head;
                    head = node;
                }

                size++;
            }

            //O(1)
            public void addLast(T item) {
                Node node = new Node(item);
                if(isEmpty())
                    head = tail = node;
                else {
                    tail.next = node;
                    tail = node;
                }

                size++;
            }

            //O(n)
            public int indexOf(T item) {
                Node current = head;
                int index = 0;
                while(current != null) {
                    if(current.value == item)
                        return index;

                    current = current.next;
                    index++;
                }
                return -1;
            }

            //O(n)
            public boolean contains(T item) {
                return indexOf(item) != -1;
            }

            //O(1)
            public void removeFirst() {
                if(isEmpty())
                    throw new NoSuchElementException(); //like java implementation

                if(head == tail) {
                    head = tail = null;
                    size = 0;
                    return;
                }

                Node second = head.next;
                head.next = null;
                head = second;
                size--;
            }

            //O(n)
            public void removeLast() {
                if(isEmpty())
                    throw new NoSuchElementException(); //like java implementation

                if(head == tail) {
                    head = tail = null;
                    size = 0;
                    return;
                }

                Node current = head;
                while(current != null) {
                    if(current.next == tail) {
                        current.next = null;
                        tail = current;
                    }
                    current = current.next;
                }
                size--;
            }

            public int size() {
                return size;
            }
        }

### Stack
![](https://github.com/shamy1st/data-structure/blob/main/images/stack.png)

--    | push | pop | peek | isEmpty
------|------|-----|------|--------
Stack | O(1) | O(1)| O(1) | O(1)

        public class Main {
            public static void main(String[] args) {
                Stack<Integer> stack = new Stack<>(10);
                stack.push(10);
                stack.push(20);
                stack.push(30);
                System.out.println(stack.pop());
                System.out.println(stack.peek());
                System.out.println(stack.isEmpty());
            }
        }

        public class Stack<T> {
            private T[] items;
            private int count;

            public Stack(int capacity) {
                items = (T[]) new Object[capacity];
            }

            public boolean isEmpty() {
                return count == 0;
            }

            public void push(T item) {
                if(count >= items.length)
                    items = (T[]) new Object[items.length * 2];
                items[count++] = item;
            }

            public T pop() {
                if(isEmpty())
                    throw new EmptyStackException();
                return items[--count];
            }

            public T peek() {
                if(isEmpty())
                    throw new EmptyStackException();
                return items[count-1];
            }
        }

### Queue
![](https://github.com/shamy1st/data-structure/blob/main/images/queue.png)

--                    | enqueue     | dequeue     | peek | isEmpty | isFull
----------------------|-------------|-------------|------|---------|-------
Queue                 | O(1)        | O(1)        | O(1) | O(1)    | O(1)
PriorityQueue (Array) | O(n)        | O(1)        | O(1) | O(1)    | O(1)
PriorityQueue (Heap)  | O(log n)    | O(log n)    | O(1) | O(1)    | O(1)

* **Queue Interface**
  * **with ArrayDeque** (Double Ended Queue)
  * **with LinkedList** 

        public class Main {
            public static void main(String[] args) {
                Queue<Integer> queue = new ArrayDeque<>();

                queue.add(10); //enqueue item, if queue is full throw exception
                queue.offer(20); //enqueue item, doesn't throw exception

                queue.remove(); //dequeue item, if queue is empty throw exception
                queue.poll(); //dequeue item, doesn't throw exception

                queue.element(); //return front item, if queue is empty throw exception
                queue.peek(); //return front item, if queue is empty return null
            }
        }

* **Reverse a Queue** (using Stack)

        public class Main {
            public static void main(String[] args) {
                Queue<Integer> queue = new ArrayDeque<>();
                queue.add(10);
                queue.add(20);
                queue.add(30);
                System.out.println(queue);
                System.out.println(reverse(queue));
            }

            public static Queue<Integer> reverse(Queue<Integer> queue) {
                Stack<Integer> stack = new Stack<>();
                while(!queue.isEmpty())
                    stack.push(queue.remove());

                while(!stack.isEmpty())
                    queue.add(stack.pop());

                return queue;
            }
        }

* **Queue Implementation**
  * **with Array**
  
        public class Main {
            public static void main(String[] args) {
                Queue<Integer> queue = new Queue<>(5);
                queue.enqueue(10);
                queue.enqueue(20);
                queue.enqueue(30);
                queue.dequeue();
                System.out.println(queue);
            }
        }

        public class Queue<T> {
            private T[] items;
            private int front;
            private int rear;
            private int count;

            public Queue(int capacity) {
                items = (T[]) new Object[capacity];
            }

            public void enqueue(T item) {
                if(count == items.length)
                    throw new IllegalStateException();
                items[rear] = item;
                rear = (rear + 1) % items.length;
                count++;
            }

            public T dequeue() {
                if(count == 0)
                    throw new NullPointerException();
                count--;
                T item = items[front];
                items[front] = null;
                front = (front + 1) % items.length;
                return item;
            }

            public boolean isEmpty() {
                return count == 0;
            }

            public boolean isFull() {
                return count == items.length;
            }

            @Override
            public String toString() {
                return "Queue{" + Arrays.toString(items) + "}";
            }
        }
  
  * **with LinkedList**
  
  * **with Stack**
  
        public class Main {
            public static void main(String[] args) {
                Queue<Integer> queue = new Queue<>();
                queue.enqueue(10);
                queue.enqueue(20);
                queue.enqueue(30);
                System.out.println(queue.dequeue());
            }
        }

        public class Queue<T> {
            private Stack<T> enqueueStack;
            private Stack<T> dequeueStack;

            public Queue() {
                enqueueStack = new Stack<>();
                dequeueStack = new Stack<>();
            }

            //O(1)
            public void enqueue(T item) {
                enqueueStack.push(item);
            }

            //O(n)
            public T dequeue() {
                if (isEmpty())
                    throw new IllegalStateException();

                if(dequeueStack.isEmpty()) {
                    while (!enqueueStack.isEmpty())
                        dequeueStack.push(enqueueStack.pop());
                }
                return dequeueStack.pop();
            }

            public boolean isEmpty() {
                return enqueueStack.isEmpty() && dequeueStack.isEmpty();
            }
        }
  
* **Priority Queue**: items are sorted

  * **with Array**
  
        public class Main {
            public static void main(String[] args) {
                PriorityQueue queue = new PriorityQueue(5);
                queue.add(5);
                queue.add(3);
                queue.add(1);
                queue.add(2);
                queue.add(4);
                System.out.println(queue.remove());
                System.out.println(queue.remove());
                System.out.println(queue);
            }
        }

        public class PriorityQueue {
            private int[] items;
            private int count;

            public PriorityQueue(int capacity) {
                items = new int[capacity];
            }

            //O(n)
            public void add(int item) {
                if(isFull())
                    throw new IllegalStateException();

                //O(n)
                int index = shiftItemsToInsert(item);
                items[index] = item;
                count++;
            }

            //O(1)
            public int remove() {
                if(isEmpty())
                    throw new NullPointerException();

                int item = items[count-1];
                items[--count] = 0;
                return item;
            }

            public boolean isEmpty() {
                return count == 0;
            }

            public boolean isFull() {
                return count == items.length;
            }

            @Override
            public String toString() {
                return "PriorityQueue{" + Arrays.toString(items) + "}";
            }

            private int shiftItemsToInsert(int item) {
                int index;
                for(index=count-1;index>=0;index--) {
                    items[index+1] = items[index];
                    if(items[index] < item) {
                        break;
                    }
                }
                return index+1;
            }
        }
  
  * **with Heap**
  
        public class PriorityQueue<T extends Number & Comparable<T>> {
            private Heap<T> heap;

            public PriorityQueue(int capacity) {
                heap = new Heap<T>(capacity);
            }

            public void enqueue(T item) {
                heap.insert(item);
            }

            public T dequeue() {
                return heap.remove();
            }

            public boolean isEmpty() {
                return heap.isEmpty();
            }

            public boolean isFull() {
                return heap.isFull();
            }
        }

### Hashing
![](https://github.com/shamy1st/data-structure/blob/main/images/hashtable.png)

--  | put | remove | get | containsKey | containsValue
----|-----|--------|-----|-------------|--------------
Map | O(1)| O(1)   | O(1)| O(1)        | O(n)

* **Interview Problems**
  * **First Non-Repeated Character**

          public class Main {
              public static void main(String[] args) {
                  System.out.println(findFirstNonRepeatedChar("a green apple")); //g
              }

              public static Character findFirstNonRepeatedChar(String str) {
                  Map<Character, Integer> map = new HashMap<>();

                  for(char ch : str.toCharArray()) {
                      int count = map.containsKey(ch) ? map.get(ch) : 0;
                      map.put(ch, count+1);
                  }

                  for(char ch : str.toCharArray()) {
                      if(map.get(ch) == 1)
                          return ch;
                  }
                  return null;
              }
          }

  * **First Repeated Character**

          public class Main {
              public static void main(String[] args) {
                  System.out.println(findFirstRepeatedChar("a green apple")); //e
              }

              public static Character findFirstRepeatedChar(String str) {
                  Set<Character> set = new HashSet<>();

                  for(char ch : str.toCharArray()) {
                      if(set.contains(ch))
                          return ch;
                      set.add(ch);
                  }
                  return null;
              }
          }

* **Collisions**
![](https://github.com/shamy1st/data-structure/blob/main/images/collisions.png)

  * **Chaining**
  ![](https://github.com/shamy1st/data-structure/blob/main/images/chaining.png)
  
        public class Main {
            public static void main(String[] args) {
                HashTable hashtable = new HashTable(5);
                hashtable.put(1, "A");
                hashtable.put(2, "B");
                hashtable.put(3, "C");
                hashtable.put(4, "D");
                hashtable.put(5, "E");
                hashtable.put(6, "F");
                hashtable.put(1, "Z");

                System.out.println(hashtable.get(4));
                System.out.println(hashtable.get(8));

                hashtable.remove(4);
                //hashtable.remove(9);

                hashtable.print();
            }
        }

        public class HashTable<K, V> {
            private class Entry<K, V> {
                private K key;
                private V value;

                public Entry(K key, V value) {
                    this.key = key;
                    this.value = value;
                }

                @Override
                public String toString() {
                    return "Entry{" + key + ", " + value + "}";
                }
            }

            private LinkedList<Entry<K, V>>[] items;

            public HashTable(int capacity) {
                items = new LinkedList[capacity];
            }

            public void put(K key, V value) {
                int bucketIndex = hash(key);
                if(items[bucketIndex] == null)
                    items[bucketIndex] = new LinkedList<>();

                for(var entry : items[bucketIndex]) {
                    if(entry.key == key) {
                        entry.value = value;
                        return;
                    }
                }
                items[bucketIndex].add(new Entry(key, value));
            }

            public V get(K key) {
                int bucketIndex = hash(key);
                if(items[bucketIndex] == null)
                    return null;

                for(var entry : items[bucketIndex]) {
                    if(entry.key == key) {
                        return entry.value;
                    }
                }
                return null;
            }

            public void remove(K key) {
                int bucketIndex = hash(key);
                if(items[bucketIndex] == null)
                    throw new IllegalStateException();

                for(var entry : items[bucketIndex]) {
                    if(entry.key == key) {
                        items[bucketIndex].remove(entry);
                        return;
                    }
                }
                throw new IllegalStateException();
            }

            private int hash(K key) {
                return key.hashCode() % items.length;
            }

            public void print() {
                for(int i=0;i<items.length;i++) {
                    if(items[i] != null) {
                        System.out.println(i + " : " + items[i].toString());
                    } else {
                        System.out.println(i + " : " + null);
                    }
                }
            }
        }
  
  * **Open Addressing**
  ![](https://github.com/shamy1st/data-structure/blob/main/images/probing.png)
  
    * **Linear Probing**
    ![](https://github.com/shamy1st/data-structure/blob/main/images/linear-probing.png)
    
    * **Quadratic Probing**
    ![](https://github.com/shamy1st/data-structure/blob/main/images/quadratic-probing.png)
    ![](https://github.com/shamy1st/data-structure/blob/main/images/quadratic-probing-2.png)
    
    * **Double Hashing**
    ![](https://github.com/shamy1st/data-structure/blob/main/images/double-hashing.png)
    ![](https://github.com/shamy1st/data-structure/blob/main/images/double-hashing-2.png)

## Non-Linear Data-Structure

### Binary Tree
![](https://github.com/shamy1st/data-structure/blob/main/images/binary-tree-example.png)

### Binary Search Tree
![](https://github.com/shamy1st/data-structure/blob/main/images/binary-search-tree.png)

average/worst      |        indexing | search          | add             | remove(index or value)
-------------------|-----------------|-----------------|-----------------|-----------------------
Binary Search Tree | O(log n) / O(n) | O(log n) / O(n) | O(log n) / O(n) | O(log n) / O(n)

* **Traversing**

  * **Breadth First**
  ![](https://github.com/shamy1st/data-structure/blob/main/images/breadth-first.png)
  
  * **Depth First**
  ![](https://github.com/shamy1st/data-structure/blob/main/images/depth-first.png)
  
    * **Pre-Order**
    ![](https://github.com/shamy1st/data-structure/blob/main/images/pre-order.png)
    
    * **In-Order**
    ![](https://github.com/shamy1st/data-structure/blob/main/images/in-order.png)
    
    * **Post-Order**
    ![](https://github.com/shamy1st/data-structure/blob/main/images/post-order.png)
    
* **Depth**: number of edges from root to the target node. (root depth = 0)

* **Height** the longest path to a leaf. (leaf node height = 0) (Post-Order Traversal)

* **Minimum Value** left left left till find leaf node. O(log n)

* **Maximum Value** right right right till find leaf node. O(log n)

* **Equality** check that two trees are totally equals.

* **Validation** given a binary tree, validate that it is a binary search tree.

        public class Main {
            public static void main(String[] args) {
                BinarySearchTree<Integer> tree = new BinarySearchTree<>();
                tree.insert(7);
                tree.insert(4);
                tree.insert(9);
                tree.insert(1);
                tree.insert(6);
                tree.insert(8);
                tree.insert(10);
                System.out.println(tree.find(8));
                tree.traverseInOrder();
                System.out.println("height: " + tree.height());
                System.out.println("min: " + tree.min());
                System.out.println("max: " + tree.max());
                System.out.println("isEqual: " + tree.equals(null));
                System.out.println("isValid: " + tree.isBinarySearchTree());
                System.out.println("NodesAtDistance : " + tree.getNodesAtDistance(2));
                tree.traverseBreadthFirst();
            }
        }

        public class BinarySearchTree<T extends Comparable<T>> {
            private class Node<T extends Comparable<T>> {
                private T value;
                private Node<T> left;
                private Node<T> right;

                public Node(T value, Node<T> left, Node<T> right) {
                    this.value = value;
                    this.left = left;
                    this.right = right;
                }

                @Override
                public String toString() {
                    return value.toString();
                }
            }

            private Node<T> root;

            public BinarySearchTree() {

            }

            //O(log n)
            public void insert(T value) {
                if(root == null)
                    root = new Node<T>(value,null, null);

                Node<T> current = root;
                while(true) {
                    if(value.compareTo(current.value) < 0) {
                        if(current.left == null) {
                            current.left = new Node<T>(value, null, null);
                            break;
                        } else {
                            current = current.left;
                        }
                    } else if(value.compareTo(current.value) > 0) {
                        if(current.right == null) {
                            current.right = new Node<T>(value, null, null);
                            break;
                        } else {
                            current = current.right;
                        }
                    } else {
                        //equal: nothing to do
                        break;
                    }
                }
            }

            //O(log n)
            public boolean find(T value) {
                Node<T> current = root;
                while(current != null) {
                    if(value.compareTo(current.value) == 0) {
                        return true;
                    } else if(value.compareTo(current.value) < 0) {
                        current = current.left;
                    } else {
                        current = current.right;
                    }
                }
                return false;
            }

            public void traversePreOrder() {
                traversePreOrder(root);
            }

            private void traversePreOrder(Node<T> node) {
                if(node == null)
                    return;

                System.out.println(node.value);
                traversePreOrder(node.left);
                traversePreOrder(node.right);
            }

            public void traverseInOrder() {
                traverseInOrder(root);
            }

            private void traverseInOrder(Node<T> node) {
                if(node == null)
                    return;

                traverseInOrder(node.left);
                System.out.println(node.value);
                traverseInOrder(node.right);
            }

            public void traversePostOrder() {
                traversePostOrder(root);
            }

            private void traversePostOrder(Node<T> node) {
                if(node == null)
                    return;

                traversePostOrder(node.left);
                traversePostOrder(node.right);
                System.out.println(node.value);
            }

            public int height() {
                return height(root);
            }

            private int height(Node<T> node) {
                if(node == null)
                    return -1;

                return 1 + Math.max(height(node.left), height(node.right));
            }

            public T min() {
                if(root == null)
                    throw new IllegalStateException();
                return minBinarySearchTree(root);
            }

            //O(log n)
            //min value for "Binary Search Tree"
            private T minBinarySearchTree(Node<T> node) {
                if(node.left == null)
                    return node.value;

                return minBinarySearchTree(node.left);
            }

            public T max() {
                if(root == null)
                    throw new IllegalStateException();
                return maxBinarySearchTree(root);
            }

            //O(log n)
            //max value for "Binary Search Tree"
            private T maxBinarySearchTree(Node<T> node) {
                if(node.right == null)
                    return node.value;

                return maxBinarySearchTree(node.right);
            }

            //O(n)
            //min value for "Binary Tree"
            private T minBinaryTree(Node<T> node) {
                if(node.left == null && node.right == null)
                    return node.value;
                else if(node.left == null)
                    return minValue(node.value, minBinaryTree(node.right));
                else if(node.right == null)
                    return minValue(node.value, minBinaryTree(node.left));

                return minValue(node.value, minValue(minBinaryTree(node.left), minBinaryTree(node.right)));
            }

            private T minValue(T value1, T value2) {
                if(value1.compareTo(value2) < 0)
                    return value1;
                return value2;
            }

            public boolean equals(BinarySearchTree<T> other) {
                if(other == null)
                    return false;
                return equals(root, other.root);
            }

            private boolean equals(Node<T> node1, Node<T> node2) {
                if(node1 == null && node2 == null)
                    return true;

                if(node1 != null && node2 != null)
                    return node1.value.compareTo(node2.value) == 0
                            && equals(node1.left, node2.left)
                            && equals(node1.right, node2.right);

                return false;
            }

            public boolean isBinarySearchTree() {
                if(root == null)
                    return true;
                return isBinarySearchTree(root);
            }

            private boolean isBinarySearchTree(Node<T> node) {
                if(node.left == null && node.right == null)
                    return true;
                else if(node.left == null && node.right != null)
                    return node.value.compareTo(node.right.value) < 0 && isBinarySearchTree(node.right);
                else if(node.left != null && node.right == null)
                    return node.value.compareTo(node.left.value) > 0 && isBinarySearchTree(node.left);

                return node.value.compareTo(node.left.value) > 0
                        && node.value.compareTo(node.right.value) < 0
                        && isBinarySearchTree(node.left) && isBinarySearchTree(node.right);
            }

            //to check non binary search tree
            public void swapRoot() {
                Node temp = root.left;
                root.left = root.right;
                root.right = temp;
            }

            public ArrayList<T> getNodesAtDistance(int k) {
                ArrayList<T> list = new ArrayList<>();
                getNodesAtDistance(root, k, list);
                return list;
            }

            private void getNodesAtDistance(Node<T> node, int distance, ArrayList<T> list) {
                if(node == null)
                    return;
                if(distance == 0) {
                    list.add(node.value);
                    return;
                }

                getNodesAtDistance(node.left, distance-1, list);
                getNodesAtDistance(node.right, distance-1, list);
            }

            //Level Order
            public void traverseBreadthFirst() {
                for(int i=0;i<=height(); i++) {
                    getNodesAtDistance(i).forEach(item -> System.out.println(item));
                }
            }
        }

* **Balanced Binary Tree**  abs[ height(left) - height(right) ] <= 1

* **Unbalanced Binary Tree**
![](https://github.com/shamy1st/data-structure/blob/main/images/unbalanced-binary-tree.png)
![](https://github.com/shamy1st/data-structure/blob/main/images/right-skewed.png)
![](https://github.com/shamy1st/data-structure/blob/main/images/left-skewed.png)

* **Self-Balancing Trees**
  * **AVL Tree** (Adelson-Velsky and Landis)
  * **Red-Black Tree**
  * **B-Tree**
  * **Splay Tree**
  * **2-3 Tree**

### AVL Tree


average/worst      |        indexing     | search              | add                 | remove(index or value)
-------------------|---------------------|---------------------|---------------------|-----------------------
AVL Tree           | O(log n) / O(log n) | O(log n) / O(log n) | O(log n) / O(log n) | O(log n) / O(log n)

* **Rotations**
  * **Left (LL)**
  ![](https://github.com/shamy1st/data-structure/blob/main/images/left-rotation-1.png)
  ![](https://github.com/shamy1st/data-structure/blob/main/images/left-rotation-2.png)
  
  * **Right (RR)**
  ![](https://github.com/shamy1st/data-structure/blob/main/images/right-rotation-1.png)
  ![](https://github.com/shamy1st/data-structure/blob/main/images/right-rotation-2.png)
  
  * **Left-Right (LR)**
  ![](https://github.com/shamy1st/data-structure/blob/main/images/left-right-rotation-1.png)
  ![](https://github.com/shamy1st/data-structure/blob/main/images/left-right-rotation-2.png)
  ![](https://github.com/shamy1st/data-structure/blob/main/images/left-right-rotation-3.png)
  
  * **Right-Left (RL)**
  ![](https://github.com/shamy1st/data-structure/blob/main/images/right-left-rotation-1.png)
  ![](https://github.com/shamy1st/data-structure/blob/main/images/right-left-rotation-2.png)
  ![](https://github.com/shamy1st/data-structure/blob/main/images/right-left-rotation-3.png)

        public class Main {
            public static void main(String[] args) {
                AVLTree<Integer> tree = new AVLTree<>();
                tree.insert(30);
                tree.insert(20);
                tree.insert(10);
            }
        }

        public class AVLTree<T extends Comparable<T>> {
            private class Node<T extends Comparable<T>> {
                private T value;
                private Node<T> left;
                private Node<T> right;
                private int height;

                public Node(T value, Node<T> left, Node<T> right, int height) {
                    this.value = value;
                    this.left = left;
                    this.right = right;
                    this.height = height;
                }

                @Override
                public String toString() {
                    return value.toString();
                }
            }

            private Node<T> root;

            public AVLTree() {

            }

            public void insert(T value) {
                root = insert(root, value);
            }

            private Node<T> insert(Node<T> node, T value) {
                if(node == null)
                    node = new Node(value, null, null, 0);
                else if(value.compareTo(node.value) < 0)
                    node.left = insert(node.left, value);
                else if(value.compareTo(node.value) > 0)
                    node.right = insert(node.right, value);

                setHeight(node);
                return balance(node);
            }

            private Node<T> balance(Node<T> node) {
                //left heavy case1: rightRotate(30)
                //    30
                //  20  (1)
                //10
                //left heavy case2: leftRotate(20) then rightRotate(30)
                //    30
                //  20  (-1)
                //    25
                if(isLeftHeavy(node)) {
                    if(balanceFactor(node.left) < 0)
                        node.left = leftRotate(node.left);
                    return rightRotate(node);
                }
                //right heavy case1: leftRotate(10)
                //10
                //  20 (-1)
                //    30
                //right heavy case2: rightRotate(20) then leftRotate(10)
                //10
                //  20 (1)
                //15
                else if(isRightHeavy(node)) {
                    if(balanceFactor(node.right) > 0)
                        node.right = rightRotate(node.right);
                    return leftRotate(node);
                }

                return node;
            }

            // 10 (node)            20 (newNode)
            //     20      ->  10      30
            //   15  30           15
            // leftRotate(10)
            private Node<T> leftRotate(Node<T> node) {
                Node<T> newNode = node.right;
                node.right = newNode.left;
                newNode.left = node;

                setHeight(node);
                setHeight(newNode);
                return newNode;
            }

            //     30 (node)           20 (newNode)
            //  20           ->    10      30
            //10  25                     25
            // leftRotate(30)
            private Node<T> rightRotate(Node<T> node) {
                Node<T> newNode = node.left;
                node.left = newNode.right;
                newNode.right = node;

                setHeight(node);
                setHeight(newNode);
                return newNode;
            }

            private int balanceFactor(Node<T> node) {
                return (node == null) ? 0 : height(node.left) - height(node.right);
            }

            private boolean isLeftHeavy(Node<T> node) {
                return balanceFactor(node) > 1;
            }

            private boolean isRightHeavy(Node<T> node) {
                return balanceFactor(node) < -1;
            }

            private void setHeight(Node<T> node) {
                node.height = 1 + Math.max(height(node.left), height(node.right));
            }

            private int height(Node<T> node) {
                return (node == null) ? -1 : node.height;
            }
        }

### Heap

* **complete** all levels must be filled from left to right.
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-complete-1.png)
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-complete-2.png)

* **incomplete**
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-incomplete-1.png)
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-incomplete-2.png)

* **heap property** each node greater than or equal to its childs.
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-property.png)
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-property-invalid.png)

* **bubble up**
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-bubble-up.png)

* **bubble down**
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-bubble-down.png)

* **complexity**
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-insert-complexity.png)

--                 |        indexing     | search              | add                 | remove
-------------------|---------------------|---------------------|---------------------|-----------------------
Heap               | O(log n)            | O(log n)            | O(log n)            | O(log n)


* **array index**
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-array-index.png)

* **applications**

  * **heap sort**
    * insert all array elments to a heap
    * remove one by one and put them to the array in order
    * now you have sorted array
    
  * **priority queue**
    * look at PriorityQueue section with Heap
    
  * **heapify** is transform an array to a heap in place.

        public class Main {
            public static void main(String[] args) {
                Integer[] array = {5, 3, 8, 4, 1, 2};
                CustomHeap.heapify(array);
                System.out.println(Arrays.toString(array)); //[8, 4, 5, 3, 1, 2]
            }
        }

        public class CustomHeap {
            public static <T extends Number & Comparable<T>> void heapify(T[] array) {
                int lastParentIndex = array.length / 2 - 1;
                for(int i=lastParentIndex;i>=0;i--) {
                    bubbleDown(array, i);
                }
            }

            private static <T extends Number & Comparable<T>> void bubbleDown(T[] array, int index) {
                while(index < array.length && !isValidParent(array, index)) {
                    swap(array, index, largerChildIndex(array, index));
                    index = largerChildIndex(array, index);
                }
            }

            private static <T extends Number & Comparable<T>> boolean isValidParent(T[] array, int index) {
                if(!hasLeftChild(array, index))
                    return true;

                if(!hasRightChild(array, index))
                    return array[index].compareTo(array[leftIndex(index)]) >= 0;

                return array[index].compareTo(array[leftIndex(index)]) >= 0
                        && array[index].compareTo(array[rightIndex(index)]) >= 0;
            }

            private static <T extends Number & Comparable<T>> void swap(T[] array, int index1, int index2) {
                T temp = array[index1];
                array[index1] = array[index2];
                array[index2] = temp;
            }

            private static <T extends Number & Comparable<T>> int largerChildIndex(T[] array, int index) {
                if(!hasLeftChild(array, index))
                    return index;

                if(!hasRightChild(array, index))
                    return leftIndex(index);

                return (array[leftIndex(index)].compareTo(array[rightIndex(index)]) > 0)
                        ? leftIndex(index) : rightIndex(index);
            }

            private static <T extends Number & Comparable<T>> boolean hasLeftChild(T[] array, int index) {
                return leftIndex(index) < array.length;
            }

            private static <T extends Number & Comparable<T>> boolean hasRightChild(T[] array, int index) {
                return rightIndex(index) < array.length;
            }

            private static int parentIndex(int index) {
                return (index - 1) / 2;
            }

            private static int leftIndex(int index) {
                return 2 * index + 1;
            }

            private static int rightIndex(int index) {
                return 2 * index + 2;
            }
        }

  * **Kth Largest Item**
    * insert all array items in heap
    * then remove (k-1) items from heap
    * the root of heap now is the Kth item

### Trie
![](https://github.com/shamy1st/data-structure/blob/main/images/trie.png)
![](https://github.com/shamy1st/data-structure/blob/main/images/trie-complexity.png)

--                 | search              | add                 | remove
-------------------|---------------------|---------------------|-----------------------
Trie               | O(L)                | O(L)                | O(L)

* **Traversals**
  * **Pre-Order** print word in forward order.
  * **Post-Order** print word in reverse order.

        public class Main {
            public static void main(String[] args) {
                Trie trie = new Trie();
                trie.insert("car");
                trie.insert("card");
                trie.insert("care");
                trie.insert("careful");
                trie.insert("egg");
                System.out.println(trie.findWords(null));
            }
        }

        public class Trie {
            private class Node {
                private char value;
                private HashMap<Character, Node> children;
                private boolean endOfWord;

                public Node(char value) {
                    this.value = value;
                    children = new HashMap<>();
                }

                public boolean hasChild(char ch) {
                    return children.containsKey(ch);
                }

                public void addChild(char ch) {
                    children.put(ch, new Node(ch));
                }

                public Node getChild(char ch) {
                    return children.get(ch);
                }

                public Node[] getChildren() {
                    return children.values().toArray(new Node[0]);
                }

                public boolean hasChildren() {
                    return !children.isEmpty();
                }

                public void setEndOfWord(boolean endOfWord) {
                    this.endOfWord = endOfWord;
                }

                public boolean isEndOfWord() {
                    return endOfWord;
                }

                @Override
                public String toString() {
                    return "Node{" + value + "}";
                }

                public void removeChild(char ch) {
                    children.remove(ch);
                }
            }

            private Node root;

            public Trie() {
                root = new Node('\0');
            }

            public void insert(String word) {
                Node current = root;
                for(char ch : word.toCharArray()) {
                    if(!current.hasChild(ch))
                        current.addChild(ch);
                    current = current.getChild(ch);
                }
                current.setEndOfWord(true);
            }

            public boolean contains(String word) {
                if(word == null)
                    return false;

                Node current = root;
                for(char ch : word.toCharArray()) {
                    if(!current.hasChild(ch))
                        return false;
                    current = current.getChild(ch);
                }

                return current.isEndOfWord();
            }

            public void traverse() {
                traversePreOrder(root);
            }

            private void traversePreOrder(Node node) {
                for(Node child : node.getChildren()) {
                    System.out.println(child.value);
                    traversePreOrder(child);
                }
            }

            private void traversePostOrder(Node node) {
                for(Node child : node.getChildren()) {
                    traversePostOrder(child);
                    System.out.println(child.value);
                }
            }

            public void remove(String word) {
                if(word == null)
                    return;

                remove(root, word, 0);
            }

            private void remove(Node node, String word, int index) {
                if(index == word.length()) {
                    node.setEndOfWord(false);
                    return;
                }

                Node child = node.getChild(word.charAt(index));
                if(child == null)
                    return;

                remove(child, word, index+1);
                if(!child.hasChildren() && !child.isEndOfWord())
                    node.removeChild(child.value);
            }

            public List<String> findWords(String prefix) {
                if(prefix == null)
                    return null;

                Node lastNode = findLastNodeOf(prefix);
                List<String> list = new ArrayList<>();
                findWords(lastNode, prefix, list);
                return list;
            }

            private void findWords(Node node, String prefix, List<String> list) {
                if(node == null)
                    return;

                if(node.isEndOfWord())
                    list.add(prefix);

                for(Node child : node.getChildren()) {
                    findWords(child, prefix + child.value, list);
                }
            }

            private Node findLastNodeOf(String prefix) {
                Node current = root;
                for(char ch : prefix.toCharArray()) {
                    Node child = current.getChild(ch);
                    if(child == null)
                        return null;
                    current = child;
                }
                return current;
            }
        }

### Graph
![](https://github.com/shamy1st/data-structure/blob/main/images/directed-graph.png)

* **Complexity** if you have dense graph use matrix implementation otherwise use list implementation.

![](https://github.com/shamy1st/data-structure/blob/main/images/dense-graph.png)

average          | add edge  | remove edge| query edge| find neighbors| add node      | remove node   | space
-----------------|-----------|------------|-----------|---------------|---------------|---------------|----------------
Adjacency Matrix | O(1)      | O(1)       | O(1)      | O(V)          | O(V^2)        | O(V^2)        | O(V^2)
Adjacency List   | O(K)      | O(K)       | O(K)      | O(K)          | O(1)          | O(V^2)        | O(V + E)

worst            | add edge  | remove edge| query edge| find neighbors| add node      | remove node   | space
-----------------|-----------|------------|-----------|---------------|---------------|---------------|----------------
Adjacency Matrix | O(1)      | O(1)       | O(1)      | O(V)          | O(V^2)        | O(V^2)        | O(V^2)
Adjacency List   | O(V)      | O(V)       | O(V)      | O(V)          | O(1)          | O(V^2)        | O(V^2)

  * **Average**
  ![](https://github.com/shamy1st/data-structure/blob/main/images/graph-complexity-average.png)
  
  * **Worst Case**
  ![](https://github.com/shamy1st/data-structure/blob/main/images/graph-complexity-worst.png)

* **Implementation**
  * **Adjacency Matrix**
  ![](https://github.com/shamy1st/data-structure/blob/main/images/graph-matrix.png)
  
  * **Adjacency List**
  ![](https://github.com/shamy1st/data-structure/blob/main/images/graph-list.png)

* **Traversals**
  * **Depth First**
  ![](https://github.com/shamy1st/data-structure/blob/main/images/graph-depth-first.png)
  
  * **Breadth First**
  ![](https://github.com/shamy1st/data-structure/blob/main/images/graph-breadth-first-1.png)
  ![](https://github.com/shamy1st/data-structure/blob/main/images/graph-breadth-first-2.png)
  
* **Topological Sort** the right order that we need to process a nodes of a graph.
  * like schedule jobs
  * doesn't produce a unique solution.
  * only for directed acyclic graphs. acyclic means without cycles.
  * nodes with outgoing edges should comes first, and nodes without any outgoing edges comes last.
  
  * How it work?
    1. traverse Depth First and go deep to the last node, add this node to stack. 
        * [X -> A -> P]
    2. go back to nodes that this node comes from and push them one by one, but after their children.
        * push P
        * push "children of A" then push A
        * push "children of X", in this case push B but also after push "children of B"
        * push X
    3. pop all elements from the stack, this is the correct order.
        * pop X
        * pop B
        * pop A
        * pop P
  
  ![](https://github.com/shamy1st/data-structure/blob/main/images/graph-topological-sort.png)

* **Cycle Detection**
![](https://github.com/shamy1st/data-structure/blob/main/images/graph-cycle-1.png)
![](https://github.com/shamy1st/data-structure/blob/main/images/graph-cycle-2.png)

        public class Main {
            public static void main(String[] args) {
                Graph graph = new Graph();
                graph.addNode("A");
                graph.addNode("B");
                graph.addNode("C");
                graph.addEdge("A", "B");
                graph.addEdge("B", "C");
                graph.addEdge("C", "A");
                System.out.println(graph.hasCycle());
            }
        }

        public class Graph {
            private class Node {
                private String label;

                public Node(String label) {
                    this.label = label;
                }

                @Override
                public String toString() {
                    return label;
                }
            }

            private Map<String, Node> nodes;
            private Map<Node, List<Node>> adjacencyList;

            public Graph() {
                this.nodes = new HashMap<>();
                this.adjacencyList = new HashMap<>();
            }

            public void addNode(String label) {
                Node node = new Node(label);
                nodes.putIfAbsent(label, node);
                adjacencyList.putIfAbsent(node, new ArrayList<>());
            }

            public void addEdge(String from, String to) {
                if(!nodes.containsKey(from) || !nodes.containsKey(to))
                    throw new IllegalStateException();

                Node fromNode = nodes.get(from);
                Node toNode = nodes.get(to);

                adjacencyList.get(fromNode).add(toNode);
            }

            public void removeNode(String label) {
                if(!nodes.containsKey(label))
                    return;

                Node node = nodes.get(label);
                for(Node fromNode : adjacencyList.keySet())
                    adjacencyList.get(fromNode).remove(node);

                adjacencyList.remove(node);
                nodes.remove(label);
            }

            public void removeEdge(String from, String to) {
                if(!nodes.containsKey(from) || !nodes.containsKey(to))
                    return;

                Node fromNode = nodes.get(from);
                Node toNode = nodes.get(to);
                adjacencyList.get(fromNode).remove(toNode);
            }

            public void print() {
                for(Node node : adjacencyList.keySet())
                    System.out.println(node + " is connected to " + adjacencyList.get(node));
            }

            public void traverseDepthFirst(String start) {
                if(!nodes.containsKey(start))
                    return;

                Node startNode = nodes.get(start);
                traverseDepthFirstRecursive(startNode, new HashSet<>());
            }

            private void traverseDepthFirstRecursive(Node node, Set<Node> visited) {
                System.out.println(node);
                visited.add(node);
                for(Node child : adjacencyList.get(node)) {
                    if(!visited.contains(child))
                        traverseDepthFirstRecursive(child, visited);
                }
            }

            public void traverseDepthFirstIterative(String start) {
                if(!nodes.containsKey(start))
                    return;

                Node startNode = nodes.get(start);

                Set<Node> visited = new HashSet<>();
                Stack<Node> stack = new Stack<>();
                stack.push(startNode);

                while(!stack.isEmpty()) {
                    Node current = stack.pop();
                    System.out.println(current);
                    visited.add(current);

                    for(Node child : adjacencyList.get(current)) {
                        if(!visited.contains(child))
                            stack.push(child);
                    }
                }
            }

            public void traverseBreadthFirst(String start) {
                if(!nodes.containsKey(start))
                    return;

                Node startNode = nodes.get(start);

                Set<Node> visited = new HashSet<>();
                Queue<Node> queue = new ArrayDeque<>();
                queue.add(startNode);

                while(!queue.isEmpty()) {
                    Node current = queue.remove();
                    System.out.println(current);
                    visited.add(current);

                    for(Node child : adjacencyList.get(current)) {
                        if(!visited.contains(child))
                            queue.add(child);
                    }
                }
            }

            public List<String> topologicalSort() {
                Set<Node> visited = new HashSet<>();
                Stack<Node> stack = new Stack<>();

                for(Node node : nodes.values())
                    topologicalSort(node, visited, stack);

                List<String> sorted = new ArrayList<>();
                while(!stack.isEmpty())
                    sorted.add(stack.pop().label);

                return sorted;
            }

            private void topologicalSort(Node node, Set<Node> visited, Stack<Node> stack) {
                if(visited.contains(node))
                    return;

                visited.add(node);

                for(Node child : adjacencyList.get(node))
                    topologicalSort(child, visited, stack);

                stack.push(node);
            }

            public boolean hasCycle() {
                Set<Node> all = new HashSet<>();
                all.addAll(nodes.values());

                Set<Node> visiting = new HashSet<>();
                Set<Node> visited = new HashSet<>();

                while(!all.isEmpty()) {
                    Node current = all.iterator().next();
                    if(hasCycle(current, all, visiting, visited))
                        return true;
                }
                return false;
            }

            private boolean hasCycle(Node node, Set<Node> all, Set<Node> visiting, Set<Node> visited) {
                all.remove(node);
                visiting.add(node);

                for(Node child : adjacencyList.get(node)) {
                    if (visited.contains(child))
                        continue;

                    if (visiting.contains(child))
                        return true;

                    if(hasCycle(child, all, visiting, visited))
                        return true;
                }

                visiting.remove(node);
                visited.add(node);

                return false;
            }
        }

### Undirected Graph

* **Dijstra**
![](https://github.com/shamy1st/data-structure/blob/main/images/dijstra-1.png)
![](https://github.com/shamy1st/data-structure/blob/main/images/dijstra-2.png)

        public class WeightedGraph {
            private class Node {
                private String label;
                private List<Edge> edges;

                public Node(String label) {
                    this.label = label;
                    this.edges = new ArrayList<>();
                }

                public void addEdge(Node to, int weight) {
                    edges.add(new Edge(this, to, weight));
                }

                public List<Edge> getEdges() {
                    return edges;
                }

                @Override
                public String toString() {
                    return label;
                }
            }

            private class NodeEntry {
                private Node node;
                private int priority;

                public NodeEntry(Node node, int priority) {
                    this.node = node;
                    this.priority = priority;
                }
            }

            private class Edge {
                private Node from;
                private Node to;
                private int weight;

                public Edge(Node from, Node to, int weight) {
                    this.from = from;
                    this.to = to;
                    this.weight = weight;
                }

                @Override
                public String toString() {
                    return from + "->" + to;
                }
            }

            private Map<String, Node> nodes;

            public WeightedGraph() {
                this.nodes = new HashMap<>();
            }

            public void addNode(String label) {
                nodes.putIfAbsent(label, new Node(label));
            }

            public void addEdge(String from, String to, int weight) {
                if(!nodes.containsKey(from) || !nodes.containsKey(to))
                    throw new IllegalStateException();

                Node fromNode = nodes.get(from);
                Node toNode = nodes.get(to);

                fromNode.addEdge(toNode, weight);
                toNode.addEdge(fromNode, weight);
            }

            public void print() {
                for(Node node : nodes.values())
                    System.out.println(node + " is connected to " + node.getEdges());
            }

            public Path getShortestPath(String from, String to) {
                Node fromNode = nodes.get(from);
                Node toNode = nodes.get(to);

                Map<Node, Integer> distances = new HashMap<>();
                for(Node node : nodes.values())
                    distances.put(node, Integer.MAX_VALUE);
                distances.replace(fromNode, 0);

                Map<Node, Node> previousNodes = new HashMap<>();

                Set<Node> visited = new HashSet<>();

                PriorityQueue<NodeEntry> queue = new PriorityQueue<>(
                        Comparator.comparingInt(entry -> entry.priority)
                );
                queue.add(new NodeEntry(fromNode, 0));

                while(!queue.isEmpty()){
                    Node current = queue.remove().node;
                    visited.add(current);

                    for(Edge edge : current.getEdges()){
                        if(visited.contains(edge.to))
                            continue;

                        int newDistance = distances.get(current) + edge.weight;
                        if(newDistance < distances.get(edge.to)) {
                            distances.replace(edge.to, newDistance);
                            previousNodes.put(edge.to, current);
                            queue.add(new NodeEntry(edge.to, newDistance));
                        }
                    }
                }

                return buildPath(toNode, previousNodes);
            }

            private Path buildPath(Node toNode, Map<Node, Node> previousNodes) {
                Stack<Node> stack = new Stack<>();
                stack.push(toNode);
                Node previous = previousNodes.get(toNode);
                while(previous != null) {
                    stack.push(previous);
                    previous = previousNodes.get(previous);
                }

                Path path = new Path();
                while(!stack.isEmpty())
                    path.add(stack.pop().label);
                return path;
            }
        }

* **Cycle Detection**

* **Minimum Spanning Tree**
![](https://github.com/shamy1st/data-structure/blob/main/images/minimum-spanning-tree-1.png)
![](https://github.com/shamy1st/data-structure/blob/main/images/minimum-spanning-tree-2.png)

  * **Prim's Algorithm**
  ![](https://github.com/shamy1st/data-structure/blob/main/images/prim-algorithm-1.png)
  ![](https://github.com/shamy1st/data-structure/blob/main/images/prim-algorithm-2.png)

## Advanced
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
