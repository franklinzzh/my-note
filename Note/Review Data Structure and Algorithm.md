

# **Review Data Structure and Algorithm**

#  Course Topics Overview 

## -Review Basic

##### static:

`static` means **“belongs to the class, not to any specific object.”**

A **static method** can be called **without creating an instance** of the class.

A **non-static method** belongs to an **object** (an instance) of that class, and you must create that object first before calling it.



##### Constructor:

https://www.w3schools.com/java/java_constructors.asp

**client class**: executable, contain main method

**object class**: contain data and behavior

##### **ADT**: 

abstract definition for expected operations and behavior; Defines the input and outputs, not the implementations; ADT provides only the interface to which a data structure must adhere to.

![image-20240611122746598](D:\Code\myWeb\Note\Screenshot\image-20240611122746598.png)

##### mod  "%"

a%b :

```java
while(a > b-1)
	a -= b;//a = a-b
return a;
```

Application of % operator:

1. Obtain last digit of a number: 230857 % 10 is 7 
2. See whether a number is odd: 7 % 2 is 1, 42 % 2 is 0 
3. Limit integers to specific range: 8 % 12 is 8, 18 % 12 is 6

## -Complexity Analysis ##

Ask for **Time**, **Space**

**Time** Complexity: the worst case for the algorithm takes time.

**Space** Complexity: how much space the algorithm allocate to store data.

**Example**:

```java
void exampleFn(int n) {
    int[] nums = new int[n];
}
```

Here time & space complexity both O(n).

1. need to set up n element in an array as a value of 0.
2. an array of size n to be remembered 



##### **Big-O Notation**: O(n)

​					gives an ***upper*** bund of complexity in the ***worst*** case

Factorial Time: O(n!)

**Big-O Examples**: 

1. Finding all subsets of a set  -O(2^n)
2. Finding all permutation of a string  -O(n!)
3. Sorting using mergesort  -O(nlog(n))

**Note**: Big-O is just an upper bound. It doesn’t have to be a good upper bound

##### Big-Omega natation: Ω(n)

​						Big-Omega is a lower bound -My code takes at least this long to run

## -Asymptotic Analysis

##### Iterator

Iterator is a java interface that dictates how a collection of data should be traversed. Can only move in the forward direction and in a single pass.

**hasNext()** – returns true if the iteration has more elements yet to be examined 

**next()** – returns the next element in the iteration and moves the iterator forward to next item

```java
ArrayList<Integer> list = new ArrayList<Integer>();

//Iterator
Iterator<Integer> itr = list.iterator();
while (itr.hasNext()) {
	int item = itr.next();
}
//forloop
for (int i : list) {
	int item = i;
}
```

###### Iterator & for loop

Using an iterator gives you the ability to remove elements from the collection during iteration with the `remove` method.

```java
Iterator<Integer> itr = list.iterator();
while (itr.hasNext()) {
    int item = itr.next();
    if (item % 2 == 0) { // For example, remove even numbers
        itr.remove();
    }
}
```



# 1. Introduction to Data Structures

Source code: https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqa2hRMVl2c2ZyTTVHQ3A2OEJ1WTRyTjhGdXRZZ3xBQ3Jtc0trTExOeEZscG1OUzBkOXphXzJSN2FVOHBiaFNTMlNnVmlLUzZqYlQ0S2M0SGdNLXhlb3lqUVRyYVRYMXNBOU9Nd1FJbUZwMXJRSWE5akdFenlDMXZ5eG4xa0tVbE5JOW9XbW1IZUo0RjdmWElDNlR0NA&q=https%3A%2F%2Fgithub.com%2Fwilliamfiset%2Falgorithms&v=HV-hpvuGaC4

```java
int[] intArray = new int[5]
```

**List**:  

```java
List<String> list = new ArrayList<>();
```

1. a collection storing an ordered sequence of elements
2. elements can be added to the front, back, or elsewhere

##### **Interface**: 



##### **Arrays** 

![image-20240611141949849](D:\Code\myWeb\Note\Screenshot\image-20240611141949849.png)

Static Array: 

1. Elements are referenced by their index. 
2. Array indexing is zero-based, first element in array(0).

Dynamic Array:

1. can grow and shrink in size
1. The underlying structure of dynamic arrays is still a static array, but it automatically handles resizing and encapsulates operations like adding, deleting, searching, and modifying, making it more convenient for us to use.

```java
A.add(-7)
A.remove(4)
    
array.length       // property, not a method
array[i]           // access element
array[i] = value   // assign element
Arrays.sort(arr);
toString(array)
int[] newArr = Arrays.copyOf(arr, 10);//new length
Arrays.fill(arr, 0);
equals(a, b)
    
```

How to implement a dynamic array? Using static array

1. Create a static array with initial capacity
2. Add elements to the underlying static array
3. If exceed the capacity, then create a new static array with twice the capacity and copy the original elements into it

https://labuladong.online/algo/en/data-structure-basic/array-implement/

Dynamic Array Source code:

```java
public class Array <T> implements Iterable <T> {
	private T [] arr;
	private int len = 0; 		// length user thinks array is
	private int capacity = 0; 	// Actual array size
	
	public Array() {this(16);}
	
	public Array(int capacity) {
		if (capacity < 0) {
			throw new IllegalArgumentException("Illegal Capacity: " + capacity);
		}
		this.capacity = capacity;
		arr = (T[]) new Object[capacity];
	}
	public int size() { return len; }
	public boolean isEmpty() { return size() == 0; }
	public T get(int index)
	public void set(int index, T elem)
	
	public void clear() {
		fori {
			arr[i] = null;
		}
		len = 0;
	}
	
	public void add(T elem) {
		if (len+1 >= capacity) {
			if (capacity == 0) {
				capacity = 1;
			} else {
				capacity = 2* capacity;
			}
			T[] new_arr = (T[]) new Object[capacity];
			fori {
				new_arr[i] = arr[i];
			}
			arr = new_arr;
		}
		arr[len++] = elem;
	}
	
	public void removeAt(int rm_index) {
        if (rm_index >= len || rm_index < 0) {
            throw new IndexOutOfBoundsExecption();
        }
		T[] new_arr = (T[]) new Object[capacity];
		for (int i = 0, j = 0; i<len; i++, j++) {
            if (j != rm_index) {
                new_arr[i] = arr[j];
            } else {
                i++;
            }
		}			
        arr = new_arr;
		len--;
	}
    //the other way
    public void removeAt(int index) {
        if (count > 0) {
            for (int i = index; i < count - 1; i++) {
 
                // shift all element of right
                // side from given index in left
                array[i] = array[i + 1];
            }
            array[count - 1] = 0;
            count--;
        }
    }
}
```



## - Linked Lists 

A linked list is a sequence list of nodes that hold data with point to other nodes also containing data

![image-20240611225037010](D:\Code\myWeb\Note\Screenshot\image-20240611225037010.png)

Singly Linked: less memory, easy implement; cannot access to previous elements

Doubly Linked: can be traversed backward; take 2x memory

Remove: 

1. need two traverse pointers to keep track of the left and right
2. only need one traverse pointer

Remove tail from a singly linked list is O(n)

Remove tail from a doubly linked list is **O(1)** (it remember head & tail)

```java
//single
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

```

```java
//doubleclass Node {
    int data;
    Node next;
    Node prev;

    Node(int data) {
        this.data = data;
        this.next = null;
        this.prev = null;
    }
}

```

##### Singly LinkedList

**Create**

```
ListNode createLinkedList(int[] arr) {
    if (arr == null || arr.length == 0) {
        return null;
    }
    ListNode head = new ListNode(arr[0]);
    ListNode temp = head;
    for (int i = 1; i < arr.length; i++) {
        temp.next = new ListNode(arr[i]);
        temp = temp.next;
    }
}
```

​	Here {arr == null} and {arr.length == 0} are both important. First one makes sure the second one won't throw NullPointerException. (null.length won't exist).

**Update/get**

```java
ListNode head = createLinkedList(new int[]{1, 2, 3, 4, 5});
void updateListNode(ListNode head, int val) {
    //for loop is used to go though every elements
    //When you know exactly how many times you’ll loop
	for (ListNode p = head; p != null; p = p.next) {
        if (p.data == val) {
            p.data += 1;
        }
    }
    //while loop is better when you want to update one target.
    ListNode temp = head;
    while (temp != null) {
        if (temp.data == val) {
            temp.data += 1;
            break;
        }
        temp = temp.next;
    }
}
```

**在单链表中间插入新元素**

```java
// 创建一条单链表
ListNode head = createLinkedList(new int[]{1, 2, 3, 4, 5});
//如果没给你链表，先check if(head == null) {head = ...}
ListNode cur = head;
//想在 index=2插入新元素 data=999
for (int i = 0; i < 2; i++) {
    cur = cur.next;
}
//way 1
ListNode temp = cur.next;
cur.next = new ListNode(999);
cur.next.next = temp;
//way 2
List temp = new ListNode(999);
temp.next = cur.next;
cur.next = temp;

```

**在单链表中删除一个节点**

```java
// 创建一条单链表
ListNode head = createLinkedList(new int[]{1, 2, 3, 4, 5});
//想在 index=4删除元素
int deleteNode(ListNode head, int index) {
    if (head == null) {
        System.out.println("Empty list");
        return -1;
    }
    // Delete head
    if (index == 0) {
        int val = head.val;
        head = head.next;
        return val;
    }
    ListNode cur = head;
    for (int i = 0; i < index-1; i++) {
        if (cur.next == null) {
            System.out.println("Index Out of bound");
            return -1;
            //break;
        } 
        cur = cur.next;
    }
    int val = cur.next.data;
    if (cur.next.next != null) {
        cur.next = cur.next.next;
    } else {
        cur.next = null;
    }
    return val;
}
```

Difference between **break** and **return**

| Keyword  | What it does                            | Effect                             |
| -------- | --------------------------------------- | ---------------------------------- |
| `break`  | Exits **only the nearest loop**         | Code *after the loop* still runs   |
| `return` | Exits the **entire method** immediately | Code *after the method* is skipped |

```java
if (cur.next == null) {
    System.out.println("Index out of bounds");
    return -1;
}
cur = cur.next;
//no need for else, beacuse return already end the method
if (cur.next == null) {
    System.out.println("Index out of bounds");
    return -1;
} else {
    cur = cur.next;
}
```

```java
//避免指针错乱的潜在问题
oldHead.next = null;
```

##### Doubly LinkedList

**双链表中间插入新元素**

```java
// 创建一条双链表
DoublyListNode head = createDoublyLinkedList(new int[]{1, 2, 3, 4, 5});

// 想要插入到索引 3（第 4 个节点）
int addNode(DoublyListNode head, int index, int var) {
    DoublyListNode p = head;
    for(int i = 0; i < index-1; i++) {
        p = p.next;
    }
    DoublyListNode newNode = new DoublyListNode(var);
    newNode.prev = p;
    DoublyListNode temp = p.next;
    newNode.next = temp;
    p.next = newNode;
    temp.prev = newNode;
    
    //better way
	DoublyListNode newNode = new DoublyListNode(var);
    newNode.prev = p;
    newNode.next = p.next;
    //this smartly save one spacetime
    p.next.prev = newNode;
    p.next = newNode;
    
    return var;
}

```

```java
//delete
cur.next.next.prev = cur;
cur.next = cur.next.next;
//better way
DoublyListNode toDelete = cur.next;
cur.next = toDelete.next;
toDelete.next.prev = cur;
toDelete.next = null;
toDelete.prev = null;

```







Difference for ArrayList & LinkedList:

For add in n-th item in ArrayList, if it needs to resize, the time is O(n).

![image-20240612121405718](D:\Code\myWeb\Note\Screenshot\image-20240612121405718.png)

Use an `ArrayList` for storing and accessing data, and `LinkedList` to manipulate data.

## - Map (Dictionary)

```java
put(key, item) add item to collection indexed with key
get(key) return item associated with key
containsKey(key) return if key already in use
remove(key) remove item and associated key
size() return count of items
```

```
//Worked both for Array/LinkedMap
put()	O(n) //find key, overwrite it; otherwise create new
get()	O(n)
containsKey()	O(n)
remove()	O(n)
size()	O(1)
```



## - Stacks

A stack is a one-ended linear data structure which models a real world stack by having two primary operations, *push* and *pop*.

Last in First out

Used for DFS

Example:

-Brackets: 

```
[[{}]()]
```

-Tower of Hanoi

Source code: Use list to perform stack

```java
push(item)	//add item to top
pop()		//return and remove item at top
//retrieve or fetch the top element present on the stack
stack.peek()
size() 		//count of items
isEmpty() 	//count of items is 0?
```



## - Queues 

##### Queue

Enqueue: add an item to the back

Dequeue: when dequeue, remove the first one.

First in First out.

```java
add(item) add item to back
remove() remove and return
item at front
peek() return item at front
size() count of items
isEmpty() count of items is 0?
```

Example: 

1. Web server request management
2. BFS graph traversal

*TO DO: Perform Queue based on stack array*

##### **Deque**

A double-ended queue, add/remove from both ends, get in middle

- Deque can act as both Stack and Queue
- It is useful in many problems where we need to have a subset of all operations also like insert/remove at front and insert/remove at the end.
- It is typically implemented either using a doubly linked list or circular array.

Sentinel Nodes: 

![image-20240612142334560](D:\Code\myWeb\Note\Screenshot\image-20240612142334560.png)



##### **Heap** 

A heap is a tree based Data Structure (**DS**) that satisfies the heap invariant: If A is a parent node of B then A is ordered with respect to B -- for all nodes A, B in the heap. (Binary Heap, Binomial Heap, Fibonacci Heap)

- **In a Max-Heap**: 

  The value of **A (parent)** is **greater than or equal to** the value of **B (child)**.

  ​								A>= B

- **In a Min-Heap**:
  The value of **A (parent)** is **less than or equal to** the value of **B (child)**.

  ​								A<=B

Note: **Siblings (nodes with the same parent)** are not ordered with respect to each other. The heap property only applies directly between parents and children.

**Heap invariant:** Every node is less than or equal to both of its children.

The heap invariant is looser than the BST(Binary Search) invariant.

**Heap structure invariant**: A heap is always a complete tree, that every row, except possibly the last, is completely full.



### **二叉堆**

##### **Priority Queue** [ADT] 

```java
class MyPriorityQueue {
    // 在二叉堆堆顶插入一个元素，时间复杂度 O(logN)
    // N 为当前二叉堆中的元素个数
    void push(int x);// 返回堆顶元素，时间复杂度 O(1)
    // 该堆顶元素就是二叉堆中的最大值或最小值，取决于是最大堆还是最小堆
    int peek();

    // 删除堆顶元素，时间复杂度 O(logN)
    int pop();

    // 返回堆中元素的个数，时间复杂度 O(1)
    int size();
}
```


A PQ is a **ADT** that each elements has a certain priority.  The priority of the elements in the priority queue determine the order in which elements are removed from the PQ.

Note: PQ only supports comparable data

How machine could sort the queue each time to poll()?

That's ineffective. It uses **heap**.

![image-20240615130754240](D:\Code\myWeb\Note\Screenshot\image-20240615130754240.png)

Example: 

1. Used in certain implementation of Dijkstra's shortest Path algorithm
2. dynamically fetch the next 'best'/'worst' element
3. Huffman coding
4. Best First Search (BFS) algorithm, such as A* use PQs
5. Minimum Spanning Tree (MST)

**Turning Min PQ into Max PQ:**

1. > For a min PQ, if x<=y, then x comes out of the PQ before y; Now the negation of this is x>=y, that x comes out first (**question**)

2. the other way is negate the number and negate again when they are taken out.

##### **Heap Sort**

乱序的数组都 `push` 到一个二叉堆（优先级队列）里面，然后再一个个 `pop` 出来，就得到了一个有序的数组

```java
// 堆排序伪码，对 arr 原地排序
// 时间复杂度 O(NlogN)，空间复杂度 O(N)
int[] heapSort(int[] arr) {
    int[] res = new int[arr.length];
    MyPriorityQueue pq = new MyPriorityQueue();
    for (int x : arr)
        pq.push(x);
    // 元素出堆的顺序是有序的
    for (int i = 0; i < arr.length; i++)
        res[i] = pq.pop();
    return res;
}
```

当然，正常的堆排序算法的代码并不依赖优先级队列，且空间复杂度是 O(1)*O*(1)。那是因为它把 `push` 和 `pop` 的代码逻辑展开了，再加上直接在数组上原地建堆，这样就不需要额外的空间了。

但堆排序的本质还是依靠二叉堆的性质来排序元素

刚才不是说二叉堆是一种特殊的二叉树吗？可视化面板中显示的二叉堆也是二叉树的形态，怎么可能不使用额外的空间复杂度，直接在数组上原地创建二叉树呢？

这个问题很好，我在 [学习数据结构和算法的框架思维](https://labuladong.online/algo/essential-technique/algorithm-summary/) 中有阐述其中的原因。

二叉树是一种逻辑概念，并不是说只有 `TreeNode` 类构造出来的那个结构才是二叉树，其实数组也可以抽象成一棵树，一切分治穷举的思想都可以抽象成一棵树，递归函数的那个递归栈也可以理解成一棵树。



##### **Binary Heap**

A binary tree that supports the heap invariant(property). In a binary tree every node has exactly two children.

 **Binary Heap invariant**: 

1. Binary Tree
2. Heap
3. Structure complete

![image-20240612233013312](D:\Code\myWeb\Note\Screenshot\image-20240612233013312.png)

```
Let i be the parent node index
Left child index: 2i+1
Right child index: 2i+2
```

**Complete** binary tree: a tree in which at every level, except the last is completely filled and all the nodes are as far left as possible.

**Adding elements into Binary Heap**: 

**Implementing add()**

1. Insert a node on the bottom level
2. Fix heap invariant by percolate **up**

**Removing elements into Binary Heap**: 

```java
poll() 		//O(log(n))
remove()	//O(n) 
    		//this has to perform a linear search to find out
```

**Implementing removeMin()**

1. Return min
2. Replace with bottom level right-most node
3. percolateDown()
   1. Recursively swap parent with **smallest** child until parent is smaller than both children (or at a leaf)

![image-20240615191844663](D:\Code\myWeb\Note\Screenshot\image-20240615191844663.png)



## -Recursion

##### Master Theorem

<img src="D:\Code\myWeb\Note\Screenshot\image-20240614205712785.png" alt="image-20240614205712785" style="zoom:50%;" />

![image-20240614205940161](D:\Code\myWeb\Note\Screenshot\image-20240614205940161-17184329725524.png)

##### Binary Search

Runtime for sorted array: 
$$
2^x  =N
$$

$$
x = log_2N
$$



##### Merge Sort

```java
mergeSort(input) {
	if (input.length == 1)
		return
	else
		smallerHalf = mergeSort(new [0, ..., mid])
		largerHalf = mergeSort(new [mid + 1, ...])
	return merge(smallerHalf, largerHalf)
}
```

Runtime: Θ(nlogn)

##### Fibonacci

```java
public int fib(int n) {
	if (n <= 1) {
		return 1;
	}
	return fib(n-1) + fib(n-1);
}
```

T(n) = 2T(n-1) + c 
$$
T(n) = (2^n-1)*T(1)
$$
Runtime: Θ(2^n)



## -Hashing 

###### 基本原理

```java
// 哈希表伪码逻辑
class MyHashMap {

    private Object[] table;

    // 增/改，复杂度 O(1)
    public void put(K key, V value) {
        int index = hash(key);
        table[index] = value;
    }

    // 查，复杂度 O(1)
    public V get(K key) {
        int index = hash(key);
        return table[index];
    }

    // 删，复杂度 O(1)
    public void remove(K key) {
        int index = hash(key);
        table[index] = null;
    }

    // 哈希函数，把 key 转化成 table 中的合法索引
    // 时间复杂度必须是 O(1)，才能保证上述方法的复杂度都是 O(1)
    private int hash(K key) {
        // ...
    }
}
```

[`key` 是唯一的，`value` 可以重复]

A hash function is any function that can be used to map *<u>data</u>* of arbitrary size to fixed-size values.

**Hashtable**: it provides a constant time lookup and update from a mapping from a key to a value

##### Hash Functions:

1. % table size
2. 

##### Hash Obsession: Collisions

Collision: multiple keys translate to the same location of the array

Big idea: the fewer the collisions, the better the runtime.

##### Fix collision: 

- Separate Chaining: If multiple things hash to the same index, then we’ll just put all of those in that same index bucket. Often, you’ll see the data structure chosen is a linked-list like structure.

put/get/containsKey almost always will have the same complexity.

If a lot of loop iterations to find the key in the bucket, our code will run slower.

It turns out we still want to resize “every so often” to make sure the average/expected length of each bucket is a small number.

![image-20240614222019893](D:\Code\myWeb\Note\Screenshot\image-20240614222019893-17184329689083.png)

##### Java and Hash Function

Object class includes default functionality: - equals - hashCode

If you want to implement your own hashCode you should: - Override BOTH hashCode() and equals()

 a.equals(b) then a.hashCode() == b.hashCode() MUST also be true

## - == and .equals()

**Using `==`:**

- **Reference Comparison (Objects)**: When comparing two objects, `==` checks whether the two references point to the exact same object in memory. It doesn't check the content or state of the objects.
- **Primitive Types**: For primitive types (e.g., `int`, `char`, `boolean`), `==` compares the actual values.

 **Using `.equals()`:**

- **Content Comparison (Objects)**: The `.equals()` method is used to compare the content of two objects. By default, the `.equals()` method in the `Object` class behaves like `==` (i.e., it compares references), but many classes (like `String`, `Integer`, etc.) override it to compare the actual data inside the objects.
- **Custom Classes**: When you create your own class, you can override the `.equals()` method to define what it means for two instances of your class to be "equal."

**Example:** 

For a HashMap<Char, Integer>, why I have to use `HashMap1.get('c').equals(HashMap2.get('c'))`? 

Why I cannot use == to compare these two integer?



In Java, when comparing `Integer` objects (or any other objects), using `==` checks for reference equality, not value equality. This means `==` checks if two references point to the same object in memory. However, when you use `.equals()`, it checks for logical equality based on the object's content.

Here's a breakdown:

1. **Reference Equality (`==`)**:
   - `==` checks if both references point to the same object instance.
   - For `Integer`, `==` can sometimes work because of integer caching in Java (typically for values between -128 and 127). However, this is not guaranteed to be reliable for all values, especially for larger values.
2. **Value Equality (`.equals()`)**:
   - `.equals()` checks if the values of the two `Integer` objects are the same.
   - It is a more reliable way to compare values because it compares the actual content of the objects.

Here's an example to illustrate:

```
javaCopy codeHashMap<Character, Integer> map1 = new HashMap<>();
HashMap<Character, Integer> map2 = new HashMap<>();
map1.put('c', 100);
map2.put('c', 100);

Integer value1 = map1.get('c'); // value1 is 100
Integer value2 = map2.get('c'); // value2 is 100

// Using == for comparison (may work for small values due to caching)
boolean sameReference = (value1 == value2); // This might be true due to caching, but not guaranteed

// Using .equals() for comparison
boolean sameValue = value1.equals(value2); // This is the correct way to compare values
```

In most cases, especially when dealing with objects like `Integer`, it is better to use `.equals()` to ensure that you are comparing the actual values rather than just checking if the references are the same.



## - Trees 

##### **Binary Tree**

A tree data structure where each node has at most **two children** — a left child and a right child. There is **no specific order** for the node values.

```java
public class Node<K> {
	K data;
	Node<K> left;
	Node<K> right;
}
```

###### DFS

```java
class TreeNode {
    int val;
    TreeNode left, right;
}
void traverse (TreeNode root) {
    if (root == null) {
        return;
    }
    //前序位置
    traverse(root.left);
    //中序位置
    traverse(root.right);
    //后序位置
}

// N 叉树的遍历框架
void traverse(Node root) {
    if (root == null) {
        return;
    }
    // 前序位置
    for (Node child : root.children) {
        traverse(child);
    }
    // 后序位置
}
```

BFS中，中序遍历结果是有序的

###### BFS

```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    //constructor
    TreeNode(int val) {
        this.val = val;
    }
}
//写法一
class BinaryTree {
    TreeNode root;
    static BinaryTree(TreeNode root) {
        this.root = root;
    }
    void BFS() {
        int height = 1;//set root heigth = 1
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        while (!q.isEmpty()) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                TreeNode cur = q.poll();
                System.out.println("val: " + cur.val 
                                   + "height: " + height);
                if (cur.left != null) {
                   q.offer(cur.left);
                }
                if (cur.right != null) {
                    q.offer(cur.right);
                }
            }
            height++;
        }
    }
    public static void main(String[] args) {
    	TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.right.right = new TreeNode(5);

        // call static method directly
        BinaryTree tree = new BinaryTree(root);
        tree.BFS();
	}
}
```

```java
//写法二
class State {
    TreeNode node;
    int depth;
    State(TreeNode node, int depth) {
        this.node = node;
        this.depth = depth;
    }
}
void BFS(TreeNode root) {
    if (root == null) {
        return;
    }
    Queue<State> q = new LinkedList<>();
    q.offer(new State(root, 1));
    while (!q.isEmpty()) {
        int size = q.size();
        for (int i = 0; i < size; i++) {
            State cur = q.poll
                ;
            TreeNode cur_node = cur.node;
            int depth = cur.depth;
            System.out.println("Node: " + cur_node 
                               + "; depth: " + depth);
            if (cur_node.left != null) {
               q.offer(new State(cur_node.left, depth + 3));
            }
            if (cur_node.left != null) {
              q.offer(new State(cur_node.right, depth + 2));
            }
        }
    }
}
```

Root node: the single node with no parent, “top” of the tree.

Leaf node: a node with no children

Subtree: a node and all it descendants

Height: 

1. OverallRoot = 7	-height = 0
2. OverallRoot = null	-height = -1

![image-20240614225606036](D:\Code\myWeb\Note\Screenshot\image-20240614225606036.png)

##### Binary Search Tree (BST)

Invariants (A.K.A. rules for your DS or algorithm)

**BST invariants:**

-For every node with key k:

1. -The left subtree has only keys smaller than k.
2. The right subtree has only keys greater than k.

Want to make a tree implement the Map ADT?

```java
public class Node<K, V> {
	K key;
	V value;
	Node<K, V> left;
	Node<K, V> right;
}
```

```java
public boolean containsKeyBST(node, key) {
	if (node == null) {
		return false;
	} else if (node.key == key) {
		return true;
	} else {
		if (key <= node.key) {
			return containsKeyBST(node.left);
		} else {
		return containsKeyBST(node.right);
		}
	}
}
```

**BST different states**:

1. Perfectly balanced: for every node, its descendants are split evenly between left and right subtrees.
2. Degenerate: for every node, all of its descendants are in the right subtree.

How are we going to make this simpler / more efficient? **Height**

**Invariants**: When writing it,  think about is it strong enough to make our code as efficient as we want?

1. Root Balanced: The root must have the same number of nodes in its left and right subtrees	(Too Weak)
2. Recursively Balanced: Every node must have the same number of nodes in its left and right subtrees.    (Too Strong)

##### AVL Tree

A Binary Search Tree that also maintains the AVL Invariant

**AVL invariant**: For every node, the height of its left subtree and right subtree differ by at most 1. 

![image-20240614232625400](D:\Code\myWeb\Note\Screenshot\image-20240614232625400.png)

A valid AVL tree: Binary Tree-->BST-->Balanced

 Self-Balancing BSTs: https://en.wikipedia.org/wiki/Self-balancing_binary_search_tree

![image-20240615111612089](D:\Code\myWeb\Note\Screenshot\image-20240615111612089.png)

![image-20240615114022081](D:\Code\myWeb\Note\Screenshot\image-20240615114022081.png)





## -VS

##### Heap VS BST:

1. Since heaps only enforce a parent-child relationship without regulating sibling or cross-level comparisons, they are **looser** than BSTs.
2. A BST has a stricter ordering, making it ideal for sorted data operations, while a heap is optimized for quick access to the maximum or minimum element.
3. **Heaps** are always **complete binary trees**

##### Binary heap VS Binary tree:

​	Binary Heap: 

1. Always a complete binary tree
2. 

​	Binary Tree: 

1. Can be balanced, unbalanced, full, complete, or perfect.
2. No specific order is required for the node values.

##### AVL VS Heaps







## - Graphs 

##### Intro

![image-20240615200552353](D:\Code\myWeb\Note\Screenshot\image-20240615200552353.png)

G = (V, E)

**Graph Direction**:

1. Undirected graph: edges have no direction and are two-way
2. Directed graph

**Degree of Vertex**: 

1. Degree: number of edges connected to that vertex
2. In-degree: the number of directed edges that point to a vertex
3. Out-degree

**Connected**: If all the vertices are connected, we say the graph is connected

**Path**:

1. A **simple path** is a path without repeated vertices
2. A **cycle** is a path whose first and last vertices are the same - A graph with a cycle is **cyclic**

**Adjacency List**:

![image-20240615203204935](D:\Code\myWeb\Note\Screenshot\image-20240615203204935.png)

**Graph problems**:

1. s-t Path. Is there a path between vertices s and t? 
2. Connectivity. Is the graph connected? 
3. Biconnectivity. Is there a vertex whose removal disconnects the graph? 
4. Shortest s-t Path. What is the shortest path between vertices s and t? 
5. Cycle Detection. Does the graph contain any cycles? 
6. Euler Tour. Is there a cycle that uses every edge exactly once? 
7. Hamilton Tour. Is there a cycle that uses every vertex exactly once? 
8. Planarity. Can you draw the graph on paper with no crossing edges? 
9. Isomorphism. Are two graphs the same graph (in disguise)?



# 2. Useful Idea

## -Palindromes

e.g. "racecar", "madam"

 1. Using for loop

    ```java
    public static boolean isPalindrome(String str) {
        for (int i = 0; i < str.length()/2; i++) {
            if (str.charAt(i) != str.charAt(str.length()-i-1)) {
                return false;
            }
        }
        return true;
    }
    ```

    

 2. Using recursion

    ```java
    public static boolean isPalindrome(String str, int left, int right) {
            if (left >= right) {
                return true;  // Base case: all characters have been checked
            }
            if (str.charAt(left) != str.charAt(right)) {
                return false;  // Characters do not match
            }
            return isPalindrome(str, left + 1, right - 1);  // Recurse for next characters
        }
    ```

    

# 3. Introduce to Algorithm



## - Sorting Algorithms

## - Searching Algorithms 

## - Advanced Topics

## - DP

##### [Mathematical Induction(数学归纳法)：](https://labuladong.online/algo/dynamic-programming/longest-increasing-subsequence/)

Solve state transfer relationship:

1. Definition for DP array
2. Based on `dp[0], ..., dp[i-1]`, try to solve `dp[i]`

Example: [LeetCode 300](https://leetcode.com/problems/longest-increasing-subsequence/)

## -Binary Search

##### patience sorting (耐心排序)

![img](D:\Code\myWeb\Note\Screenshot\poker2.jpeg)

Rule: 只能把点数小的牌压到点数比它大的牌上；如果当前牌点数较大没有可以放置的堆，则新建一个堆，把这张牌放进去；如果当前牌有多个堆可供选择，则选择最左边的那一堆放置。

