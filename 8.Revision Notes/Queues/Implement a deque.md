Here's a complete guide to implementing a **Non-Circular Deque (Double-Ended Queue)** using a **Doubly Linked List**, including:

- ✅ What is a Non-Circular Deque
    
- 🧠 Design considerations
    
- 🔧 Full Java code
    
- ⏱ Time and space complexity
    
- ⚠️ Edge cases
    
- 🔗 Variants and related problems
    

---

# 📘 Non-Circular Deque

---

## ✅ What Is a Non-Circular Deque?

A **Deque (Double-Ended Queue)** supports:

|Operation|Description|
|---|---|
|`insertFront(x)`|Insert `x` at the front|
|`insertLast(x)`|Insert `x` at the rear|
|`deleteFront()`|Remove element from front|
|`deleteLast()`|Remove element from rear|
|`getFront()`|Get the front element|
|`getRear()`|Get the rear element|
|`isEmpty()`|Return true if deque is empty|
|`size()`|Number of elements in deque|

Unlike circular deque:

- No wrapping around (no modulo)
    
- Dynamic size (can grow as needed)
    
- Ideal for real-world queues like undo/redo or browser history
    

---

## 🧠 Design: Doubly Linked List (Non-Circular)

- Each node has:
    
    - `val` (value)
        
    - `prev` pointer
        
    - `next` pointer
        
- Maintain:
    
    - `head` → first real node (after dummy head)
        
    - `tail` → last real node (before dummy tail)
        
    - `size` → current number of elements
        

---

## ✅ Java Implementation – Non-Circular Deque

```java
public class NonCircularDeque {
    private class Node {
        int val;
        Node prev, next;
        Node(int val) { this.val = val; }
    }

    private Node head, tail;
    private int size;

    public NonCircularDeque() {
        head = new Node(-1); // dummy head
        tail = new Node(-1); // dummy tail
        head.next = tail;
        tail.prev = head;
        size = 0;
    }

    // Insert at front
    public void insertFront(int val) {
        Node node = new Node(val);
        Node next = head.next;

        head.next = node;
        node.prev = head;
        node.next = next;
        next.prev = node;
        size++;
    }

    // Insert at rear
    public void insertLast(int val) {
        Node node = new Node(val);
        Node prev = tail.prev;

        prev.next = node;
        node.prev = prev;
        node.next = tail;
        tail.prev = node;
        size++;
    }

    // Remove from front
    public boolean deleteFront() {
        if (isEmpty()) return false;
        Node frontNode = head.next;
        head.next = frontNode.next;
        frontNode.next.prev = head;
        size--;
        return true;
    }

    // Remove from rear
    public boolean deleteLast() {
        if (isEmpty()) return false;
        Node rearNode = tail.prev;
        tail.prev = rearNode.prev;
        rearNode.prev.next = tail;
        size--;
        return true;
    }

    public int getFront() {
        return isEmpty() ? -1 : head.next.val;
    }

    public int getRear() {
        return isEmpty() ? -1 : tail.prev.val;
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public int size() {
        return size;
    }
}
```

---

## ⏱ Time & Space Complexity

|Operation|Time|Space|
|---|---|---|
|insertFront|O(1)|O(n)|
|insertLast|O(1)|O(n)|
|deleteFront|O(1)|O(n)|
|deleteLast|O(1)|O(n)|
|getFront/Rear|O(1)|O(n)|
|isEmpty|O(1)|O(1)|
|size|O(1)|O(1)|

---

## 🧪 Edge Cases to Handle

|Case|Handling|
|---|---|
|Deletion from empty|Return false|
|Access front/rear empty|Return -1|
|Only one element|Make sure both pointers adjust|
|Insert and delete mix|Always adjust links carefully|

---

## 📊 Circular vs Non-Circular Deque

|Feature|Circular (Array)|Non-Circular (Linked List)|
|---|---|---|
|Size|Fixed (bounded)|Dynamic|
|Memory use|Efficient|Slightly more (pointers)|
|Wrapping logic|Yes (`mod`)|No|
|Use case|Bounded systems|Flexible stacks, buffers|

---

## 🔗 Related Problems (Use Deque)

|Problem|Notes|
|---|---|
|Leetcode 239 – Sliding Window Maximum|Monotonic deque (linked list form)|
|GFG – Check for Palindrome|Use deque to compare both ends|
|Implement LRU Cache|Use HashMap + doubly linked deque|
|Text editor undo/redo|Use two deques|

---

## ✅ Summary

|Feature|Value|
|---|---|
|Data Structure|Doubly linked list (non-circular)|
|Insert/Delete Ends|O(1)|
|Growable|Yes (dynamic)|
|Use Cases|Undo/redo, browser history, palindromes|

---

Would you like:

- A **circular array version** for bounded use cases?
    
- A **practice sheet of deque-based problems**?
    
- A **JUnit test class** for this implementation?
    

Let me know and I’ll set it up.