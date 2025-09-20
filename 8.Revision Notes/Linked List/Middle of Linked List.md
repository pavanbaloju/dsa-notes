Here's a full DSA breakdown of the classic Linked List problem: **“Middle of the Linked List”**, with brute force to optimal approaches, **Java code**, and detailed reasoning.

---

# ✅ Problem: Middle of the Linked List

(Leetcode 876)

---

## 🔹 Problem Statement

> Given the **head** of a singly linked list, return the **middle node** of the linked list.  
> If there are two middle nodes, return the **second** one.

---

### 🔸 Example 1:

```
Input: 1 → 2 → 3 → 4 → 5  
Output: 3
```

### 🔸 Example 2:

```
Input: 1 → 2 → 3 → 4 → 5 → 6  
Output: 4 (second middle)
```

---

## 🔁 Pattern

- **Two-pass traversal**
    
- **Slow and Fast Pointer (Tortoise & Hare)**
    

---

# 🔻 Approach 1: Two-Pass Traversal

### 🔸 Step 1: Count the number of nodes `n`

### 🔸 Step 2: Traverse to node at `n / 2` and return it

---

### ✅ Java Code

```java
public ListNode middleNode(ListNode head) {
    int count = 0;
    ListNode temp = head;

    // First pass: count nodes
    while (temp != null) {
        count++;
        temp = temp.next;
    }

    // Second pass: go to middle
    temp = head;
    for (int i = 0; i < count / 2; i++) {
        temp = temp.next;
    }

    return temp;
}
```

---

### ⏱ Time & Space:

- Time: `O(n)`
    
- Space: `O(1)`
    
- ✅ Simple, but requires 2 traversals
    

---

# ✅ Approach 2: Slow and Fast Pointer (Optimal)

### 🔸 Idea:

- Slow moves 1 step
    
- Fast moves 2 steps
    
- When `fast` reaches end, `slow` is at middle
    

---

### ✅ Java Code

```java
public ListNode middleNode(ListNode head) {
    ListNode slow = head;
    ListNode fast = head;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }

    return slow;
}
```

---

### ⏱ Time & Space:

- Time: `O(n)`
    
- Space: `O(1)`
    
- ✅ Most optimal and elegant
    
- ✅ Only **1 pass**
    
- ✅ Automatically handles **even-length lists** by returning the second middle
    

---

## 🔁 Dry Run Example

### Input: `1 → 2 → 3 → 4 → 5 → 6`

|Iteration|Slow|Fast|
|---|---|---|
|0|1|1|
|1|2|3|
|2|3|5|
|3|4|null → done ✅|

Output: `4`

---

## 🧠 Edge Cases

- Single node → return that node
    
- Two nodes → return second one
    
- Even-length → return second middle by default
    

---

## 📊 Comparison Table

|Approach|Time|Space|Passes|Notes|
|---|---|---|---|---|
|Two-Pass Traversal|O(n)|O(1)|2|Easy, but redundant pass|
|✅ Slow & Fast Pointer|O(n)|O(1)|1|✅ Best for interviews|

---

## 🔗 Leetcode Link

- [Leetcode 876 – Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)
    

---

## ✅ Summary

- Use **slow and fast pointers** for most efficient and elegant solution.
    
- Great foundation for problems like:
    
    - Detect cycle in linked list
        
    - Reorder list
        
    - Reverse second half
        
    - Palindrome linked list check
        

---

Would you like:

- A reusable `LinkedListUtils` for this and similar problems?
    
- Variants like “find k-th node from end”, or “split list in halves”?