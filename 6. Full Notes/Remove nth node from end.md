## **Remove Nth Node from End of Linked List**

### **🔹 Problem Statement**

Given the **head** of a linked list, remove the **n-th node from the end** of the list and return its head.

### **🔹 Example**

#### **Input:**

```plaintext
head = [1,2,3,4,5], n = 2
```

#### **Output:**

```plaintext
[1,2,3,5]
```

#### **Explanation:**

- The **2nd node from the end** is `4`, so we remove it.
    

---

## **🔹 Approach**

### **🌟 Key Idea: Two-Pointer Technique**

Instead of calculating the length separately, we use **two pointers (fast and slow)** to directly locate the node to be removed.

### **🔹 Algorithm**

1. **Use a dummy node** before `head` to handle edge cases (like removing the first node).
    
2. **Move `fast` pointer `n+1` steps ahead**, so there is an exact `n` gap between `fast` and `slow`.
    
3. **Move both `fast` and `slow`** together until `fast` reaches `null`.
    
4. **Skip the target node** by setting `slow.next = slow.next.next`.
    

---

## **🔹 Java Code with Comments**

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

public class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        // 1️⃣ Create a dummy node before head
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        
        ListNode fast = dummy, slow = dummy;

        // 2️⃣ Move fast pointer `n+1` steps ahead
        for (int i = 0; i <= n; i++) {
            fast = fast.next;
        }

        // 3️⃣ Move both fast and slow until fast reaches the end
        while (fast != null) {
            fast = fast.next;
            slow = slow.next;
        }

        // 4️⃣ Skip the target node
        slow.next = slow.next.next;

        return dummy.next; // Return new head (skip dummy)
    }
}
```

---

## **🔹 Dry Run**

### **Example:**

```plaintext
head = [1, 2, 3, 4, 5], n = 2
```

### **Step 1️⃣: Initialize Pointers**

```plaintext
dummy → 1 → 2 → 3 → 4 → 5 → NULL
fast, slow = dummy
```

### **Step 2️⃣: Move `fast` `n+1 = 3` steps ahead**

```plaintext
fast → 3, slow → dummy
```

### **Step 3️⃣: Move both until `fast` reaches `null`**

```plaintext
fast → null, slow → 3
```

### **Step 4️⃣: Remove `4`**

```plaintext
1 → 2 → 3 → 5 → NULL
```

---

## **🔹 Time & Space Complexity**

- **Time Complexity:** `O(N)` (Single pass traversal)
    
- **Space Complexity:** `O(1)` (In-place modification)
    

---

## **🔹 Why This Works**

✅ **Handles all edge cases** (Removing the first or last node)  
✅ **Efficient single-pass solution** using the **two-pointer technique**  
✅ **Does not require extra storage**

Would you like a **recursive** version as well? 🚀