Here are **complete notes** for **Implementing a Circular Queue** (Leetcode 622), including:

- Problem statement
    
- Real-life use cases
    
- Key design decisions
    
- Java implementation
    
- Time/space complexity
    
- Visual dry run and edge cases
    

---

# 📘 Leetcode 622 – Design Circular Queue

---

## ✅ Problem Statement

> Design a circular queue with a fixed size `k`, supporting the following operations:

- `MyCircularQueue(k)` – Constructor to set capacity
    
- `enQueue(value)` – Insert value at rear. Return true if successful
    
- `deQueue()` – Delete element from front. Return true if successful
    
- `Front()` – Get the front element
    
- `Rear()` – Get the rear element
    
- `isEmpty()` – Return true if empty
    
- `isFull()` – Return true if full
    

---

## 🧠 Intuition: Why Circular?

In a normal queue implemented using an array:

- After a few enqueues and dequeues, **empty spaces build up at the front**
    
- But the tail still moves forward, eventually causing overflow
    

A **circular queue** reuses the freed-up front space by **wrapping around**.

---

## 🛠️ Design Choices

- Use a fixed-size array `arr[]`
    
- Maintain two pointers:
    
    - `front`: points to the current front element
        
    - `rear`: points to the next insertion index (rear + 1)
        
- Maintain a `count` of elements to track full/empty state
    

---

## ✅ Java Implementation

```java
class MyCircularQueue {
    private int[] data;
    private int front;
    private int rear;
    private int count;
    private int size;

    public MyCircularQueue(int k) {
        data = new int[k];
        size = k;
        front = 0;
        rear = 0;
        count = 0;
    }

    public boolean enQueue(int value) {
        if (isFull()) return false;
        data[rear] = value;
        rear = (rear + 1) % size;
        count++;
        return true;
    }

    public boolean deQueue() {
        if (isEmpty()) return false;
        front = (front + 1) % size;
        count--;
        return true;
    }

    public int Front() {
        return isEmpty() ? -1 : data[front];
    }

    public int Rear() {
        if (isEmpty()) return -1;
        int last = (rear - 1 + size) % size;
        return data[last];
    }

    public boolean isEmpty() {
        return count == 0;
    }

    public boolean isFull() {
        return count == size;
    }
}
```

---

## 🔁 Visual Dry Run (k = 3)

```text
Operations: enQueue(1), enQueue(2), enQueue(3), deQueue(), enQueue(4)

Start:
data: [_, _, _]    front = 0, rear = 0

After enQueue(1):
data: [1, _, _]    rear = 1

After enQueue(2):
data: [1, 2, _]    rear = 2

After enQueue(3):
data: [1, 2, 3]    rear = 0 (wrapped)

After deQueue():
front = 1          → 2 is now front

After enQueue(4):
data: [4, 2, 3]    rear = 1 (wrapped)
```

---

## ⏱ Time and Space Complexity

|Operation|Time|Space|
|---|---|---|
|enQueue|O(1)|O(k)|
|deQueue|O(1)|O(k)|
|Front/Rear|O(1)|O(k)|
|isEmpty|O(1)|O(1)|
|isFull|O(1)|O(1)|

---

## ⚠️ Common Edge Cases

|Case|What to Check|
|---|---|
|Rear wraps to 0|Use `(rear + 1) % size`|
|Front wraps to 0|Use `(front + 1) % size`|
|Rear is behind front|Still valid; track count properly|
|Rear = Front but count = 0|Means **empty**, not full|

---

## 🔗 Related Problems

|Problem|Type|
|---|---|
|Leetcode 641 – Design Circular Deque|Deque variant|
|GFG – First K elements reversal|Queue + stack|
|Leetcode 933 – Number of Recent Calls|Simulate with queue|

---

## ✅ Summary

|Concept|Value|
|---|---|
|Data Structure|Array with modulo wraparound|
|Queue behavior|FIFO with bounded size|
|Key operations|Modulo-based pointer movement|
|Extras|Track count for full/empty|

---

Would you like:

- A **double-ended** version (Leetcode 641)?
    
- A **JUnit test class** for all operations?
    
- A **memory-efficient Linked List based** circular queue?
    

Let me know — I’ll build it for you.