## **Rotate a Linked List**

### **🔹 Problem Statement**

Given the **head** of a **singly linked list**, rotate the list to the **right** by `k` places.

### **🔹 Example**

#### **Input:**

```plaintext
head = [1, 2, 3, 4, 5], k = 2
```

#### **Output:**

```plaintext
[4, 5, 1, 2, 3]
```

#### **Explanation:**

- Rotating by **1 step**: `[5, 1, 2, 3, 4]`
    
- Rotating by **2 steps**: `[4, 5, 1, 2, 3]` ✅
    

---

## **🔹 Approach**

### **🌟 Key Observations**

1. **If k is greater than the length of the list,** then rotating `k` times is the same as rotating `k % length` times.
    
2. **Instead of rotating one step at a time,** we can directly:
    
    - Find the new tail and new head
        
    - Break the list and reconnect
        

---

## **🔹 Algorithm**

1. **Find the length** of the linked list (`N`).
    
2. **Compute `k % N`** to handle cases where `k > N`.
    
3. If `k == 0`, **return the head** (no rotation needed).
    
4. **Find the new tail** at position `N - k - 1` (0-based index).
    
5. **Break the list** after `newTail`, set `newHead = newTail.next`.
    
6. **Connect the old tail** to the old head to form a circular list.
    
7. **Set newTail.next = null** to break the cycle.
    

---

## **🔹 Code with Comments**

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

public class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if (head == null || head.next == null || k == 0) return head;

        // 1️⃣ Find the length of the list
        int length = 1; // Start with 1 as we count the head
        ListNode tail = head;
        while (tail.next != null) {
            tail = tail.next;
            length++;
        }

        // 2️⃣ Compute effective rotations needed
        k = k % length; // If k is a multiple of length, no rotation is needed
        if (k == 0) return head;

        // 3️⃣ Find new tail (N - k - 1 position)
        ListNode newTail = head;
        for (int i = 0; i < length - k - 1; i++) {
            newTail = newTail.next;
        }

        // 4️⃣ Set new head and break the list
        ListNode newHead = newTail.next;
        newTail.next = null;
        tail.next = head; // Connect old tail to old head

        return newHead;
    }
}
```

---

## **🔹 Dry Run**

### **Example:**

```plaintext
head = [1, 2, 3, 4, 5], k = 2
```

### **Step 1️⃣: Find Length & Last Node**

```plaintext
length = 5
tail = 5
```

### **Step 2️⃣: Compute `k % length`**

```plaintext
k = 2 % 5 = 2  (No change)
```

### **Step 3️⃣: Find New Tail (At Position `length - k - 1 = 5 - 2 - 1 = 2`)**

```plaintext
newTail = 3
```

### **Step 4️⃣: Break & Reconnect**

```plaintext
New Head → 4 → 5 → 1 → 2 → 3 → NULL
```

---

## **🔹 Time & Space Complexity**

- **Time Complexity:** `O(N)` (One pass to find length, another to find new tail)
    
- **Space Complexity:** `O(1)` (In-place modification)
    

---

## **🔹 Why This Works**

- Avoids unnecessary rotations when `k > length`.
    
- Uses **fast pointer traversal** instead of rotating step by step.
    
- Handles **edge cases efficiently**.
    

Would you like another example walkthrough? 🚀