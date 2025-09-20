Absolutely! Here’s a **comprehensive list of essential Java classes and methods** that are frequently used in **DSA problems**. Reviewing these will ensure you can write **efficient and clean code** in interviews.

---

## **1. Arrays (`java.util.Arrays`)**

Useful for sorting, searching, and manipulating arrays.

```java
import java.util.Arrays;

int[] arr = {5, 1, 9, 3};
Arrays.sort(arr);  // Sorts array in ascending order

int index = Arrays.binarySearch(arr, 3);  // Searches element (Binary Search)

int[] filledArray = new int[5];
Arrays.fill(filledArray, -1);  // Fills array with -1

int[][] deepCopiedArr = Arrays.copyOf(arr, arr.length);  // Copies array

System.out.println(Arrays.toString(arr));  // Prints array
```

---

## **2. ArrayList (`java.util.ArrayList`)**

Dynamic array alternative with useful methods.

```java
import java.util.ArrayList;
import java.util.Collections;

ArrayList<Integer> list = new ArrayList<>();
list.add(10);
list.add(5);
list.add(8);
list.remove(1);  // Removes element at index 1

Collections.sort(list);  // Sorts list

System.out.println(list.contains(8));  // Checks if 8 exists

System.out.println(list);  // Prints list
```

---

## **3. LinkedList (`java.util.LinkedList`)**

Supports efficient insertions/removals.

```java
import java.util.LinkedList;

LinkedList<Integer> linkedList = new LinkedList<>();
linkedList.add(1);
linkedList.addFirst(0);  // Adds at the beginning
linkedList.addLast(2);  // Adds at the end

System.out.println(linkedList.removeFirst());  // Removes first element

System.out.println(linkedList.removeLast());  // Removes last element
```

---

## **4. Stack (`java.util.Stack`)**

LIFO (Last-In-First-Out) operations.

```java
import java.util.Stack;

Stack<Integer> stack = new Stack<>();
stack.push(1);
stack.push(2);
stack.push(3);

System.out.println(stack.peek());  // Top element (3)

System.out.println(stack.pop());  // Removes and returns top element (3)
```

---

## **5. Queue (`java.util.Queue`) and Deque (`java.util.Deque`)**

FIFO (First-In-First-Out) operations.

```java
import java.util.LinkedList;
import java.util.Queue;

Queue<Integer> queue = new LinkedList<>();
queue.offer(10);  // Add element
queue.offer(20);
queue.offer(30);

System.out.println(queue.poll());  // Removes and returns head (10)

System.out.println(queue.peek());  // Returns head without removing (20)
```

### **Deque (Double-ended Queue)**

Efficient for sliding window problems.

```java
import java.util.Deque;
import java.util.LinkedList;

Deque<Integer> deque = new LinkedList<>();
deque.addFirst(1);
deque.addLast(2);
deque.removeFirst();
deque.removeLast();
```

---

## **6. HashMap (`java.util.HashMap`)**

Key-value storage with **O(1) average time complexity** for operations.

```java
import java.util.HashMap;

HashMap<String, Integer> map = new HashMap<>();
map.put("Alice", 25);
map.put("Bob", 30);

System.out.println(map.get("Alice"));  // Fetch value (25)

map.remove("Bob");  // Removes entry

System.out.println(map.containsKey("Alice"));  // Checks if key exists

for (String key : map.keySet()) {
    System.out.println(key + " -> " + map.get(key));
}
```

---

## **7. HashSet (`java.util.HashSet`)**

Stores unique elements and supports **O(1) average time complexity**.

```java
import java.util.HashSet;

HashSet<Integer> set = new HashSet<>();
set.add(1);
set.add(2);
set.add(3);
set.add(1);  // Duplicates are ignored

System.out.println(set.contains(2));  // Checks if element exists

set.remove(2);  // Removes element
```

---

## **8. PriorityQueue (`java.util.PriorityQueue`)**

Min-Heap (default) or Max-Heap implementation.

```java
import java.util.PriorityQueue;

PriorityQueue<Integer> minHeap = new PriorityQueue<>();
minHeap.offer(10);
minHeap.offer(5);
minHeap.offer(8);

System.out.println(minHeap.poll());  // Removes and returns smallest element (5)

// Max-Heap using custom comparator
PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);
maxHeap.offer(10);
maxHeap.offer(5);
maxHeap.offer(8);

System.out.println(maxHeap.poll());  // Removes and returns largest element (10)
```

---

## **9. TreeMap (`java.util.TreeMap`)**

Sorted key-value storage (Balanced BST - Red-Black Tree).

```java
import java.util.TreeMap;

TreeMap<Integer, String> treeMap = new TreeMap<>();
treeMap.put(2, "B");
treeMap.put(1, "A");
treeMap.put(3, "C");

System.out.println(treeMap.firstKey());  // First (smallest) key
System.out.println(treeMap.lastKey());  // Last (largest) key
```

---

## **10. String (`java.lang.String`)**

String manipulation utilities.

```java
String str = "Hello World";
System.out.println(str.length());  // String length

System.out.println(str.charAt(1));  // Get character at index

System.out.println(str.substring(0, 5));  // Get substring

System.out.println(str.contains("Hello"));  // Check if contains

System.out.println(str.split(" "));  // Split by space
```

---

## **11. StringBuilder (`java.lang.StringBuilder`)**

For efficient string manipulation.

```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");  // Append string

sb.insert(5, " Java");  // Insert at index 5

sb.reverse();  // Reverse string

System.out.println(sb.toString());
```

---

## **12. Math (`java.lang.Math`)**

Math utility methods.

```java
import java.lang.Math;

System.out.println(Math.max(10, 20));  // Max of two numbers
System.out.println(Math.min(10, 20));  // Min of two numbers
System.out.println(Math.abs(-5));  // Absolute value
System.out.println(Math.pow(2, 3));  // 2^3 = 8
System.out.println(Math.sqrt(16));  // Square root of 16
System.out.println(Math.floor(4.9));  // Floor (4.0)
System.out.println(Math.ceil(4.1));  // Ceiling (5.0)
```

---

## **13. Random (`java.util.Random`)**

For generating random numbers.

```java
import java.util.Random;

Random rand = new Random();
int randomNumber = rand.nextInt(100);  // Random number [0, 99]
System.out.println(randomNumber);
```

---

## **14. Character (`java.lang.Character`)**

Useful for working with characters.

```java
char ch = 'A';
System.out.println(Character.isDigit(ch));  // Check if digit
System.out.println(Character.isLetter(ch));  // Check if letter
System.out.println(Character.toLowerCase(ch));  // Convert to lowercase
System.out.println(Character.toUpperCase('b'));  // Convert to uppercase
```

---

### **🔥 How to Revise?**

- Go through **each of these classes once**.
- Solve **at least one problem** using each.
- If short on time, **focus on Arrays, ArrayList, HashMap, HashSet, Stack, and PriorityQueue**.

Would you like a **flashcard-style revision sheet** for these?