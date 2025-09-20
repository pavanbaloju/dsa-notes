## **Reverse Linked List II – Explanation**

### **🔹 Problem Statement**

Given the head of a **singly linked list**, reverse the nodes from position `left` to `right`, and return the modified list.

💡 **Constraints:**

- `1 ≤ left ≤ right ≤ length of list`
    
- The list **may contain multiple nodes** or even **one node**.
    

---

## **🔹 Approach & Algorithm**

To solve this problem efficiently in **O(N) time**, we use the **iterative approach with pointer manipulation**.

### **🌟 Key Idea**

- Traverse to the `left-1` node (node **before** the reversal starts).
    
- Reverse the sublist from `left` to `right` **in-place**.
    
- Reconnect the reversed sublist with the rest of the list.
    

---

## **🔹 Step-by-Step Explanation**

### **1️⃣ Initialize Pointers**

- Create a **dummy node** (`dummy` → `0 → head`). This helps handle edge cases like reversing from the head.
    
- Set `prev` to `dummy`. Move `prev` to the **node before** `left` (i.e., `left-1` node).
    

### **2️⃣ Reverse the Sublist (Between `left` and `right`)**

- Start with `curr = prev.next` (node at `left`).
    
- Reverse `right-left+1` nodes using **a standard linked list reversal**.
    

### **3️⃣ Reconnect the Reversed Part**

- Connect the **tail of reversed sublist** to the remaining part of the list.
    
- Connect `prev.next` to the **new head** of the reversed sublist.
    

---

## **🔹 Code with Comments**

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

public class Solution {
    public ListNode reverseBetween(ListNode head, int left, int right) {
        if (head == null || left == right) return head; // No need to reverse

        ListNode dummy = new ListNode(0); // Dummy node to handle edge cases
        dummy.next = head;
        ListNode prev = dummy;

        // 1️⃣ Move `prev` to the node before `left`
        for (int i = 1; i < left; i++) {
            prev = prev.next;
        }

        // 2️⃣ Start Reversing from `left` to `right`
        ListNode curr = prev.next;  // First node of the sublist
        ListNode next;
        ListNode prevSublist = null;

        for (int i = 0; i <= right - left; i++) {
            next = curr.next;  // Store next node
            curr.next = prevSublist;  // Reverse current node
            prevSublist = curr;
            curr = next;
        }

        // 3️⃣ Reconnect the reversed sublist
        prev.next.next = curr;   // Connect the tail of reversed part to `curr`
        prev.next = prevSublist; // Connect `prev` to new head of reversed sublist

        return dummy.next; // Return new head (skip dummy node)
    }
}
```

---

## **🔹 Dry Run with Example**

### **Example Input:**

```plaintext
head = [1, 2, 3, 4, 5], left = 2, right = 4
```

### **Initial Linked List**

```plaintext
1 → 2 → 3 → 4 → 5
```

We need to reverse the sublist `[2, 3, 4]`.

---

### **Step 1️⃣: Move `prev` to `left - 1`**

```plaintext
dummy → 1 → 2 → 3 → 4 → 5
            ↑ 
          prev (Node before left)
```

`prev` now points to node `1` (the node **before** `left`).

---

### **Step 2️⃣: Reverse Sublist [2, 3, 4]**

#### **Iteration 1:**

- `curr = 2`
    
- Reverse `curr → prevSublist`
    

```plaintext
dummy → 1 → 2 → NULL
        prev      curr
prevSublist → 2
```

#### **Iteration 2:**

- `curr = 3`
    
- Reverse `curr → prevSublist`
    

```plaintext
dummy → 1 → 3 → 2 → NULL
        prev      curr
prevSublist → 3 → 2
```

#### **Iteration 3:**

- `curr = 4`
    
- Reverse `curr → prevSublist`
    

```plaintext
dummy → 1 → 4 → 3 → 2 → NULL
        prev      curr
prevSublist → 4 → 3 → 2
```

---

### **Step 3️⃣: Reconnect Sublist**

Now `prevSublist = 4 → 3 → 2`, and `curr = 5`.

- Attach **tail of reversed sublist** (`2`) to `curr`
    
- Attach `prev.next` to `prevSublist`
    

```plaintext
dummy → 1 → 4 → 3 → 2 → 5
```

Final result:

```plaintext
1 → 4 → 3 → 2 → 5
```

---

## **🔹 Time & Space Complexity**

- **Time Complexity:** `O(N)` (Traverse the list once, reverse sublist in-place)
    
- **Space Complexity:** `O(1)` (No extra space used)
    

---

## **🔹 Why This Works**

1. **Moves `prev` correctly** to **before** the reversal point.
    
2. **Uses the standard linked list reversal technique**.
    
3. **Reconnects the modified sublist** properly.
    

Would you like me to break down another example? 🚀