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
### Binary Tree
### Binary Search Tree
### Heap
### Hash Table
### Hashing
### Graph

## Advanced
* Advanced Lists
* Trie
* Matrix
* Misc
* Segment Tree
* Binary Indexed Tree
* Suffix Array
* Suffix Tree
* AVL Tree
* Splay Tree
* B Tree
* Red-Black Tree
* K Dimensional Tree
