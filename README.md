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

--                 | indexing | search | add    | remove(index or value)
-------------------|----------|--------|--------|-----------------------
Basic Array        | O(1)     | O(n)   | -      | -
Dynamic Array      | O(1)     | O(n)   | O(n)   | O(n)
Singly Linked List | O(n)     | O(n)   | O(1)   | O(n)
Doubly Linked List | O(n)     | O(n)   | O(1)   | O(n)

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
### Binary Search Tree
### AVL Tree
### Heap
### Trie
### Graph

## Advanced
* Advanced Lists
* Matrix
* Misc
* Segment Tree
* Binary Indexed Tree
* Suffix Array
* Suffix Tree
* Splay Tree
* B Tree
* Red-Black Tree
* K Dimensional Tree
