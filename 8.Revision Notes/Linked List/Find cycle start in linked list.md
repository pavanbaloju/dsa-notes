## **📝 Find the Start of the Cycle in a Linked List (Leetcode 142 – Linked List Cycle II)**

### **🔹 Problem Statement**

Given the `head` of a linked list, return the **node where the cycle begins**.  
If there is **no cycle**, return `null`.

**Constraints:**

- Do **not** modify the linked list.
    
- Optimize for **time** and **space**.
    

---

## **🔹 Approaches**

### **✅ 1. Floyd’s Cycle Detection Algorithm (Two Pointers) – O(N) time, O(1) space**

#### **🔹 Intuition**

1. **Detect if there is a cycle** using **slow** and **fast pointers**.
    
2. If a cycle exists, find the **start** of the cycle:
    
    - **When slow and fast meet**, move one pointer to `head` and keep the other at the meeting point.
        
    - Move both **one step** at a time.
        
    - **Where they meet is the start of the cycle**.
        

#### **🔹 Why does this work?**

- Let `x` be the distance from `head` to the cycle start.
    
- Let `y` be the distance from cycle start to the **meeting point**.
    
- Let `C` be the cycle length.
    
- The **fast pointer** moves twice as fast as the **slow pointer**, so:
    
    - When they meet, the **fast pointer has traveled twice** the distance of the slow pointer.
        
    - This leads to the conclusion that moving **one pointer from head** and **one from the meeting point** will lead them to the cycle start at the same time.
        

#### **🔹 Algorithm**

1. Use Floyd’s Cycle Detection Algorithm to detect a cycle.
    
2. If **no cycle**, return `null`.
    
3. If a cycle exists:
    
    - Move **one pointer to `head`**.
        
    - Move both **one step at a time**.
        
    - The node where they meet is the **cycle start**.
        

---

### **🔹 Java Code**

```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if (head == null || head.next == null) return null;

        ListNode slow = head;
        ListNode fast = head;

        // Step 1: Detect if a cycle exists
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;

            if (slow == fast) {  // Cycle detected
                // Step 2: Find cycle start
                fast = head;
                while (fast != slow) {
                    fast = fast.next;
                    slow = slow.next;
                }
                return fast; // Cycle start
            }
        }
        return null; // No cycle
    }
}
```

---

### **🔹 Dry Run Example**

**Input:**  
`head → A → B → C → D → E → C (cycle)`

|Step|Slow Pointer|Fast Pointer|Meeting?|
|---|---|---|---|
|1|A|B|❌|
|2|B|D|❌|
|3|C|C|✅ (Cycle detected)|

Now, place **one pointer at `head`** and **one at meeting point (`C`)**.  
Move both **one step at a time** until they meet again at **C (cycle start)**.

---

## **🔹 Complexity Analysis**

|Approach|Time Complexity|Space Complexity|
|---|---|---|
|**Floyd’s Cycle Detection (Tortoise & Hare)**|`O(N)`|`O(1)`|

---

## **🔹 Summary**

|Approach|When to Use|
|---|---|
|**Floyd’s Cycle Detection (Tortoise & Hare)**|**Best choice** (O(N) time, O(1) space)|
|**HashSet Method** (Store visited nodes)|Not optimal due to O(N) space|

---

### **🔹 Follow-Up: How to Remove the Cycle?**

Once you find the cycle start, set `prev.next = null` to remove it.

Would you like the **removal of cycle logic** as well? 🚀