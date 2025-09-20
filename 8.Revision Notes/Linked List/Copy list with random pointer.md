# **Copy List with Random Pointer**

(Leetcode 138 – **Deep Copy of a Linked List**)

---

## **🔹 Problem Statement**

A **linked list** is given where each node contains:

- `val` → Node’s value.
    
- `next` → Pointer to the next node.
    
- `random` → Pointer to any node in the list (or `null`).
    

Your task is to **create a deep copy** of this list.

---

## **🔹 Example**

### **Input:**

```plaintext
Original List:
1 → 2 → 3 → null
random pointers:
1 → 3
2 → 1
3 → 2
```

### **Output:**

```plaintext
Copied List:
1' → 2' → 3' → null
random pointers:
1' → 3'
2' → 1'
3' → 2'
```

---

## **🔹 Approach 1: Using HashMap** (`O(N) time, O(N) space`)

### **🔹 Idea**

1. Use a **HashMap** to store `original node → copied node` mappings.
    
2. Create a **new node** for each original node and store it in the map.
    
3. Set up the `next` and `random` pointers using the map.
    

---

### **🔹 Java Code (HashMap Approach)**

```java
import java.util.HashMap;

class Node {
    int val;
    Node next, random;
    Node(int val) { this.val = val; }
}

public class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) return null;

        // Step 1: Create a mapping from original nodes to copied nodes
        HashMap<Node, Node> map = new HashMap<>();
        Node curr = head;

        while (curr != null) {
            map.put(curr, new Node(curr.val));
            curr = curr.next;
        }

        // Step 2: Assign next and random pointers
        curr = head;
        while (curr != null) {
            map.get(curr).next = map.get(curr.next);
            map.get(curr).random = map.get(curr.random);
            curr = curr.next;
        }

        return map.get(head); // Return the copied head
    }
}
```

---

## **🔹 Approach 2: Optimized O(1) Space (Interleaving Nodes)**

### **🔹 Idea**

1. **Interweave copied nodes** between original nodes.
    
2. **Assign random pointers** to copied nodes.
    
3. **Separate** the copied list from the original.
    

---

### **🔹 Java Code (Optimized O(1) Space)**

```java
class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) return null;

        // Step 1: Insert copied nodes in between original nodes
        Node curr = head;
        while (curr != null) {
            Node copy = new Node(curr.val);
            copy.next = curr.next;
            curr.next = copy;
            curr = copy.next;
        }

        // Step 2: Set up random pointers
        curr = head;
        while (curr != null) {
            if (curr.random != null) {
                curr.next.random = curr.random.next;
            }
            curr = curr.next.next;
        }

        // Step 3: Separate the copied list from the original
        Node dummy = new Node(0);
        Node copyCurr = dummy;
        curr = head;

        while (curr != null) {
            copyCurr.next = curr.next;
            curr.next = curr.next.next;
            curr = curr.next;
            copyCurr = copyCurr.next;
        }

        return dummy.next;
    }
}
```

---

## **🔹 Dry Run of Optimized Approach**

### **Original List:**

```plaintext
1 → 2 → 3 → null
random pointers:
1 → 3
2 → 1
3 → 2
```

### **Step 1: Insert copied nodes**

```plaintext
1 → 1' → 2 → 2' → 3 → 3' → null
```

### **Step 2: Assign random pointers**

```plaintext
1'.random = 3'
2'.random = 1'
3'.random = 2'
```

### **Step 3: Separate copied list**

```plaintext
Copied List:
1' → 2' → 3'
```

---

## **🔹 Complexity Analysis**

|Approach|Time Complexity|Space Complexity|
|---|---|---|
|**HashMap (`O(N)`)**|`O(N)`|`O(N)` (stores original-copy mappings)|
|**Optimized (`O(1)`)**|`O(N)`|`O(1)` (modifies in-place)|

---

## **🔹 Summary**

✅ **Best Approach:** **O(1) Space Optimized Approach**  
✅ **Time Complexity:** **O(N)**  
✅ **Space Complexity:** **O(1)**

Would you like a step-by-step visualization for better understanding? 🚀