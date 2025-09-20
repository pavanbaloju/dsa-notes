## **📝 Detect Cycle in a Linked List (Leetcode 141 – Linked List Cycle)**

### **🔹 Problem Statement**

Given the `head` of a linked list, determine if the linked list has a cycle in it.

**Constraints:**

- Do **not** modify the linked list.
    
- Optimize for **time** and **space**.
    

---

## **🔹 Approaches**

### **✅ 1. Floyd’s Cycle Detection Algorithm (Tortoise & Hare) – O(N) time, O(1) space**

#### **🔹 Intuition**

Use two pointers:

- **Slow pointer (`slow`)** moves **one step** at a time.
    
- **Fast pointer (`fast`)** moves **two steps** at a time.
    
- If there is a cycle, the fast pointer will eventually **catch up** to the slow pointer.
    
- If there is **no cycle**, the fast pointer will reach the end (`null`).
    

#### **🔹 Algorithm**

1. Initialize `slow = head`, `fast = head`.
    
2. Move `slow` by **one step** and `fast` by **two steps**.
    
3. If `fast` reaches `null`, return **false** (no cycle).
    
4. If `slow == fast`, return **true** (cycle detected).
    
5. Repeat until `fast` reaches the end.
    

#### **🔹 Java Code**

```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) return false;

        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;       // Move slow by 1 step
            fast = fast.next.next;  // Move fast by 2 steps

            if (slow == fast) return true; // Cycle detected
        }
        return false; // No cycle
    }
}
```

#### **🔹 Why does this work?**

- If there's a cycle, fast and slow pointers will **always meet** inside the cycle.
    
- If there's no cycle, fast will eventually reach `null`.
    

---

### **✅ 2. HashSet Method – O(N) time, O(N) space**

#### **🔹 Idea**

- Store each visited node in a `HashSet`.
    
- If a node is visited again, there’s a **cycle**.
    

#### **🔹 Java Code**

```java
import java.util.HashSet;

public class Solution {
    public boolean hasCycle(ListNode head) {
        HashSet<ListNode> visited = new HashSet<>();

        while (head != null) {
            if (visited.contains(head)) return true; // Cycle detected
            visited.add(head);
            head = head.next;
        }
        return false;
    }
}
```

#### **🔹 Why not use this?**

- **Uses extra space (`O(N)`)**, while Floyd’s Algorithm only uses `O(1)`.
    
- Not interview-optimal but useful for debugging.
    

---

## **🔹 Complexity Analysis**

|Approach|Time Complexity|Space Complexity|
|---|---|---|
|**Floyd’s Cycle Detection (Tortoise & Hare)**|`O(N)`|`O(1)`|
|**HashSet Method**|`O(N)`|`O(N)`|

---

## **🔹 Summary**

|Approach|When to Use|
|---|---|
|**Floyd’s Cycle Detection (Tortoise & Hare)**|**Best choice** (O(N) time, O(1) space)|
|**HashSet Method**|If modifying list is allowed, but space isn’t optimized|

---

## **🔹 Follow-Up: Find the Start of the Cycle?**

If a cycle exists, how do we find **where it starts**?  
👉 Check **Leetcode 142 – Linked List Cycle II** (Detect & Return Cycle Start Node).

Would you like a breakdown for **Leetcode 142** as well? 🚀