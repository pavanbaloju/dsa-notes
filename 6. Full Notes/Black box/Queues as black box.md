Here’s the **Black Box Learning Breakdown for Queues**, including **Java examples** and **best, average, and worst-case complexities**.

---

# **Queue – Black Box Learning Approach**

## **1. Input**

A **Queue** is a **First-In, First-Out (FIFO)** data structure where elements are **added at the rear** and **removed from the front**.

- **Enqueue (Offer):** Insert an element at the end (rear).
- **Dequeue (Poll):** Remove an element from the front.
- **Peek:** Retrieve the front element without removing it.
- **Types of Queues:**
    - **Simple Queue:** Basic FIFO behavior.
    - **Circular Queue:** Treats the array as circular to reuse space.
    - **Deque (Double-ended Queue):** Allows insertion/removal at both ends.
    - **Priority Queue:** Elements are dequeued based on priority, not order.

### **Queue Implementation in Java**

Using **Java’s Queue Interface (LinkedList-based)**:

```java
import java.util.*;

Queue<Integer> queue = new LinkedList<>();
queue.offer(10);
queue.offer(20);
queue.offer(30);
```

Using **Array Implementation**:

```java
class ArrayQueue {
    int[] arr;
    int front, rear, size, capacity;

    ArrayQueue(int capacity) {
        this.capacity = capacity;
        arr = new int[capacity];
        front = 0;
        size = 0;
        rear = capacity - 1;
    }

    void enqueue(int x) {
        if (size == capacity) throw new RuntimeException("Queue Overflow");
        rear = (rear + 1) % capacity;
        arr[rear] = x;
        size++;
    }

    int dequeue() {
        if (size == 0) throw new RuntimeException("Queue Underflow");
        int val = arr[front];
        front = (front + 1) % capacity;
        size--;
        return val;
    }
}
```

---

## **2. Output**

- **Elements processed in FIFO order.**
- **First element accessed using `peek()`.**
- **Queue becomes empty after all elements are dequeued.**

Example:

```java
System.out.println(queue.peek());  // Output: 10
queue.poll();
System.out.println(queue.peek());  // Output: 20
```

---

## **3. Operations**

### **Basic Operations**

|Operation|Example (Java)|Best Case|Average Case|Worst Case|
|---|---|---|---|---|
|**Enqueue (Insert at Rear)**|`queue.offer(x);`|**O(1)**|**O(1)**|**O(1)**|
|**Dequeue (Remove from Front)**|`queue.poll();`|**O(1)**|**O(1)**|**O(1)**|
|**Peek (Front Element)**|`queue.peek();`|**O(1)**|**O(1)**|**O(1)**|
|**Check If Empty**|`queue.isEmpty();`|**O(1)**|**O(1)**|**O(1)**|
|**Iterate Over Queue**|`for (int x : queue)`|**O(n)**|**O(n)**|**O(n)**|

---

## **4. Time and Space Complexities**

### **Time Complexity Summary**

|Operation|Best Case|Average Case|Worst Case|
|---|---|---|---|
|**Enqueue/Dequeue/Peek**|O(1)|O(1)|O(1)|
|**Iterate Over Queue**|O(n)|O(n)|O(n)|

### **Space Complexity**

- **O(n)** for storing `n` elements.

---

## **5. Use Cases**

- **Scheduling processes in operating systems (Round Robin).**
- **Handling requests in a web server.**
- **Breadth-First Search (BFS) in graphs.**
- **Print job management.**
- **Caching (FIFO-based eviction policy).**

---

## **6. Problems in this Pattern**

### **Easy**

- Implement Queue using Array or Linked List
- Reverse a Queue
- Check if a Queue is a Palindrome

### **Medium**

- Implement Circular Queue
- First Unique Character in a String
- Interleave Two Queues

### **Hard**

- Sliding Window Maximum (Monotonic Queue)
- Shortest Path in a Binary Matrix (BFS)
- Design a Task Scheduler

---

## **7. Explore - Other Related Concepts**

- **Deque (Double-Ended Queue):** Supports insertion/deletion at both ends.
- **Priority Queue:** Elements removed based on priority rather than order.
- **Stack (LIFO):** The opposite of queue behavior.
- **Breadth-First Search (BFS):** Uses queues for level-order traversal in graphs.
- **Sliding Window Problems:** Optimized using Deque or Monotonic Queue.

---

## **Conclusion**

By treating Queue as a **black box**, we:  
✅ **Observed how input changes affect output.**  
✅ **Identified patterns in operations.**  
✅ **Implemented solutions before diving into deep theory.**

Would you like to continue with **Deque, Circular Queue, or Priority Queue (Heap) next?**