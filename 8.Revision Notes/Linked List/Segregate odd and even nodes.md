Here is a complete DSA breakdown of the Linked List problem: **"Segregate Odd and Even Nodes"**, with full explanation, **brute to optimal approaches**, and clean **Java code**.

---

# ✅ Problem: Segregate Odd and Even Nodes in a Linked List

(Variation of Leetcode 328 – [Odd Even Linked List](https://leetcode.com/problems/odd-even-linked-list/))

---

## 🔹 Problem Statement

> Given a **singly linked list**, group all **odd-positioned** nodes together followed by the even-positioned nodes.  
> **Position refers to index (1-based), not value.**

You must do it in-place with `O(1)` space and `O(n)` time.

---

### 🔸 Example:

```
Input:  1 → 2 → 3 → 4 → 5  
Output: 1 → 3 → 5 → 2 → 4

Input:  2 → 1 → 3 → 5 → 6 → 4 → 7  
Output: 2 → 3 → 6 → 7 → 1 → 5 → 4
```

---

## 🔁 Pattern

- Linked list rearrangement
    
- Maintain two separate chains: odd and even
    
- Link odd → even at the end
    

---

# ✅ Optimal Approach: Two Pointers (Odd and Even Chains)

### 🔸 Idea:

- Use 3 pointers:
    
    - `odd` → head of odd-positioned nodes
        
    - `even` → head of even-positioned nodes
        
    - `evenHead` → save the start of even list
        
- Traverse while rearranging links
    

---

### ✅ Java Code:

```java
public ListNode oddEvenList(ListNode head) {
    if (head == null || head.next == null) return head;

    ListNode odd = head;
    ListNode even = head.next;
    ListNode evenHead = even;

    while (even != null && even.next != null) {
        odd.next = even.next;
        odd = odd.next;

        even.next = odd.next;
        even = even.next;
    }

    odd.next = evenHead;  // attach even list after odd list
    return head;
}
```

---

### 🔁 Dry Run

For input `1 → 2 → 3 → 4 → 5`:

- After loop:
    
    - `odd list`: `1 → 3 → 5`
        
    - `even list`: `2 → 4`
        
- Final: `1 → 3 → 5 → 2 → 4`
    

---

### ⏱ Time & Space

|Metric|Value|
|---|---|
|Time|O(n)|
|Space|O(1)|
|In-place|✅ Yes|

---

# ❗Common Mistakes

- Confusing _value_ with _position_  
    This problem is based on **node positions**, not whether the value is odd or even.
    
- Forgetting to reconnect the `odd` and `even` lists at the end
    

---

## 🧠 Edge Cases

|Case|Output|
|---|---|
|Empty list|null|
|1 node|same|
|2 nodes|same|
|Already segregated|same|
|All odd/even positions|grouped same|

---

## 🔗 Leetcode Link

- [Leetcode 328 – Odd Even Linked List](https://leetcode.com/problems/odd-even-linked-list/)
    

---

## ✅ Summary

- Use two-pointer technique with `odd`, `even`, and `evenHead`
    
- Rearranged in-place using constant space
    
- Great test of pointer manipulation and structure
    

---

### Would you like:

- A version that segregates **odd and even by value** instead of position?
    
- Java code to **build and print a linked list** for testing?
    
- Practice variants like **Rearrange in zig-zag**, **Reverse even positioned nodes**, or **Segregate 0s and 1s**?
    

Let me know!