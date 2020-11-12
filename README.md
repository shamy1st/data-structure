# Data Structure

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

--                 | addFirst | addMiddle | addLast | removeFirst | removeMiddle | removeLast
-------------------|----------|-----------|---------|-------------|--------------|-----------
Singly Linked List | O(1)     | O(n)      | O(1)    | O(1)        | O(n)         | O(n)
Doubly Linked List | O(1)     | O(n)      | O(1)    | O(1)        | O(n)         | O(1)

--    | push | pop | peek | isEmpty
------|------|-----|------|--------
Stack | O(1) | O(1)| O(1) | O(1)

--            | enqueue | dequeue | peek | isEmpty | isFull
--------------|---------|---------|------|---------|-------
Queue         | O(1)    | O(1)    | O(1) | O(1)    | O(1)
PriorityQueue | O(n)    | O(1)    | O(1) | O(1)    | O(1)

--  | put | remove | get | containsKey | containsValue
----|-----|--------|-----|-------------|--------------
Map | O(1)| O(1)   | O(1)| O(1)        | O(n)

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

--            | enqueue | dequeue | peek | isEmpty | isFull
--------------|---------|---------|------|---------|-------
Queue         | O(1)    | O(1)    | O(1) | O(1)    | O(1)
PriorityQueue | O(n)    | O(1)    | O(1) | O(1)    | O(1)

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

* **heap property**
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-property.png)
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-property-invalid.png)

* **bubble up**
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-bubble-up.png)

* **bubble down**
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-bubble-down.png)

* **complexity**
![](https://github.com/shamy1st/data-structure/blob/main/images/heap-insert-Complexity.png)

--                 |        indexing     | search              | add                 | remove
-------------------|---------------------|---------------------|---------------------|-----------------------
Heap               | O(log n)            | O(log n)            | O(log n)            | O(log n)

### Trie



### Graph



### Undirected Graph



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
