## **Intersection of Two Linked Lists**

### **🔹 Problem Statement**

Given the heads of two singly linked lists, `headA` and `headB`, return the node at which the two lists intersect. If the two linked lists have no intersection, return `null`.

### **🔹 Example**

#### **Input:**

```plaintext
headA = [4,1,8,4,5], headB = [5,6,1,8,4,5]
```

#### **Output:**

```plaintext
Intersecting at node with value 8
```

#### **Explanation:**

The two lists intersect at node **8**, after which they share the same nodes.

---

## **🔹 Approach**

### **🌟 Key Idea: Two Pointer Technique**

- Instead of using extra memory, **two pointers traverse both lists completely**.
    
- When **one pointer reaches the end**, it moves to the head of the other list.
    
- This ensures they travel **equal distances** and meet at the intersection point.
    

### **🔹 Algorithm**

1. **Initialize two pointers**, `pA` and `pB`, at `headA` and `headB`, respectively.
    
2. **Traverse both lists simultaneously.**
    
    - If `pA` reaches `null`, move it to `headB`.
        
    - If `pB` reaches `null`, move it to `headA`.
        
3. **Continue traversal until they meet** at the intersection node or both become `null`.
    

---

## **🔹 Java Code with Comments**

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) return null;

        ListNode pA = headA, pB = headB;

        // Traverse both lists
        while (pA != pB) {
            // If pA reaches end, move to headB; else move to next node
            pA = (pA == null) ? headB : pA.next;
            
            // If pB reaches end, move to headA; else move to next node
            pB = (pB == null) ? headA : pB.next;
        }
        
        return pA; // Either the intersection node or null
    }
}
```

---

## **🔹 Dry Run**

### **Example:**

```plaintext
headA:  4 → 1 → 8 → 4 → 5
headB:       5 → 6 → 1 → 8 → 4 → 5
```

### **Step 1️⃣: Initialize Pointers**

```plaintext
pA → 4, pB → 5
```

### **Step 2️⃣: Move both pointers forward**

```plaintext
pA → 1, pB → 6
pA → 8, pB → 1
pA → 4, pB → 8
pA → 5, pB → 4
pA → null, pB → 5 (End reached, switch heads)
```

### **Step 3️⃣: Switch Pointers**

```plaintext
pA → 5 (Now starts at headB)
pB → 4 (Now starts at headA)
```

### **Step 4️⃣: Move forward again until they meet**

```plaintext
pA → 6, pB → 1
pA → 1, pB → 8
pA → 8 (Intersection), pB → 8 (Intersection)
```

---

## **🔹 Time & Space Complexity**

- **Time Complexity:** `O(M + N)` (Both pointers traverse at most `M + N` nodes)
    
- **Space Complexity:** `O(1)` (No extra space used)
    

---

## **🔹 Why This Works**

✅ **Ensures both pointers travel the same distance**  
✅ **Handles different list lengths automatically**  
✅ **Does not require extra storage (like HashSet approach)**

Would you like to see the **HashSet approach** as well? 🚀