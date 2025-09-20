## **🔄 Reverse a Linked List (Leetcode 206 – Reverse Linked List)**

### **🔹 Problem Statement**

Given the `head` of a **singly linked list**, reverse the list and return the new `head`.

---

## **🔹 Approaches**

### **✅ 1. Iterative Approach (Two Pointers) – O(N) time, O(1) space**

#### **🔹 Intuition**

- Traverse the list and reverse the `next` pointers one by one.
    
- Maintain three pointers:
    
    - `prev` (previous node)
        
    - `curr` (current node)
        
    - `next` (next node to process)
        

#### **🔹 Algorithm**

1. Initialize `prev = null`, `curr = head`.
    
2. Iterate while `curr` is not `null`:
    
    - Store `next = curr.next` (save next node).
        
    - Reverse: `curr.next = prev`.
        
    - Move `prev` and `curr` forward.
        
3. Return `prev` (new head of reversed list).
    

#### **🔹 Java Code**

```java
public class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null, curr = head;
        
        while (curr != null) {
            ListNode next = curr.next;  // Store next node
            curr.next = prev;  // Reverse link
            
            prev = curr;  // Move prev forward
            curr = next;  // Move curr forward
        }
        return prev;  // New head
    }
}
```

---

## **✅ 2. Recursive Approach – O(N) time, O(N) space (Stack Recursion)**

#### **🔹 Intuition**

- Recursively reverse the sublist **starting from the second node**.
    
- Set `head.next.next = head` to reverse the link.
    
- Base case: If the list is empty or has one node, return `head`.
    

#### **🔹 Algorithm**

1. **Base case:** If `head == null` or `head.next == null`, return `head`.
    
2. Recursively reverse the sublist from `head.next` onwards.
    
3. Reverse the current link: `head.next.next = head`.
    
4. Set `head.next = null` (to avoid cycles).
    
5. Return `newHead`.
    

#### **🔹 Java Code**

```java
public class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) return head;
        
        ListNode newHead = reverseList(head.next);  // Reverse rest of list
        head.next.next = head;  // Reverse link
        head.next = null;  // Set next to null
        
        return newHead;
    }
}
```

---

## **🔹 Complexity Analysis**

|Approach|Time Complexity|Space Complexity|
|---|---|---|
|**Iterative (Two Pointers)**|`O(N)`|`O(1)`|
|**Recursive**|`O(N)`|`O(N)` (Recursion stack)|

---

## **🔹 Dry Run Example**

**Input:**  
`head → 1 → 2 → 3 → 4 → 5 → NULL`

**After Reversing:**  
`head → 5 → 4 → 3 → 2 → 1 → NULL`

|Step|Current Node (`curr`)|Previous Node (`prev`)|Next Node (`next`)|
|---|---|---|---|
|1|1|null|2|
|2|2|1|3|
|3|3|2|4|
|4|4|3|5|
|5|5|4|null|

---

## **🔹 Summary**

|Approach|When to Use|
|---|---|
|**Iterative (Two Pointers)**|Best for efficiency (`O(N) time, O(1) space`)|
|**Recursive**|Clearer logic but uses `O(N)` stack space|

Would you like to see variations like **reversing k nodes at a time** or **reversing between indices**? 🚀