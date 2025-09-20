Here is a **complete DSA breakdown** of the classic Linked List problem:

---

# ✅ Problem: Detect a Loop in Linked List and Find Its Length

(aka: _Cycle Detection + Cycle Length_)  
Leetcode Variant: [Leetcode 141 – Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

---

## 🔹 Problem Statement

> Given the head of a singly linked list:

1. **Detect if there is a cycle (loop)**
    
2. **If a cycle exists, return its length**
    

---

## 🧠 Real-World Analogy

Imagine you're walking through rooms where each door leads to another room. If you revisit a room you've been to before, you're in a **cycle**.

---

## 🧩 Pattern

- Use **Floyd’s Cycle Detection Algorithm** (Tortoise and Hare)
    
- Once the **slow and fast pointers meet**, loop is confirmed
    
- To find the **cycle length**, fix one pointer and move the other until it meets again
    

---

# ✅ Step 1: Detect if Loop Exists (Floyd’s Cycle Detection)

### ✅ Java Code:

```java
public boolean hasCycle(ListNode head) {
    ListNode slow = head;
    ListNode fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;

        if (slow == fast) return true;  // cycle found
    }

    return false;
}
```

---

# ✅ Step 2: If Cycle Exists, Find Its Length

### 🔸 Idea:

After detecting the meeting point, move one pointer in a full loop until it meets the other again — count the steps.

---

### ✅ Java Code:

```java
public int cycleLength(ListNode head) {
    ListNode slow = head;
    ListNode fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;

        if (slow == fast) {
            // Cycle found, now measure its length
            return countCycleLength(slow);
        }
    }

    return 0; // No cycle
}

private int countCycleLength(ListNode meetingPoint) {
    ListNode current = meetingPoint;
    int length = 0;

    do {
        current = current.next;
        length++;
    } while (current != meetingPoint);

    return length;
}
```

---

### ⏱ Time & Space:

|Metric|Value|
|---|---|
|Time|O(n)|
|Space|O(1)|
|Uses|2 pointers (no HashSet needed)|

---

## 🔁 Dry Run Example

### Input:

```
List: 1 → 2 → 3 → 4 → 5 → 3 (back to node with value 3)
```

- `slow` and `fast` meet at node `4`
    
- From node `4`, we loop: `4 → 5 → 3 → 4` → length = 3 ✅
    

---

## 🧠 Edge Cases

|Case|Output|
|---|---|
|Empty list|No cycle (length = 0)|
|Single node (no loop)|No cycle|
|Single node (points to self)|Cycle, length = 1|

---

## 🔗 Related Problems

|Problem|Description|
|---|---|
|LC 141|Detect cycle|
|LC 142|Find starting node of cycle|
|LC 876|Find middle node|
|LC 234|Palindrome linked list|
|LC 143|Reorder list|

---

## ✅ Summary

- Use **Floyd's algorithm** to detect loop
    
- After detection, move pointer in cycle to find its **length**
    
- No extra space required — fully in-place, O(n) time
    

---

Would you like the **code to also return the starting node** of the cycle (Leetcode 142)?  
Or a **visual explanation** with steps and pointer states?