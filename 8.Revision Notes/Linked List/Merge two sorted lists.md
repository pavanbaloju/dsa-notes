# **Merge Two Sorted Lists**

## **🔹 Problem Statement**

Given the heads of two **sorted** linked lists, `list1` and `list2`, **merge them into one sorted list**. Return the **head of the merged list**.

---

## **🔹 Example**

#### **Input:**

```plaintext
list1 = [1, 2, 4]
list2 = [1, 3, 4]
```

#### **Output:**

```plaintext
Merged List: [1, 1, 2, 3, 4, 4]
```

#### **Explanation:**

Both lists are already sorted. We merge them while **maintaining the sorted order**.

---

## **🔹 Approach**

### **✅ Iterative Two-Pointer Approach**

1. **Use a dummy node** to simplify handling edge cases.
    
2. **Use two pointers**, `p1` for `list1` and `p2` for `list2`.
    
3. **Compare nodes**:
    
    - Add the smaller node to the merged list.
        
    - Move the pointer of the list from which we took the node.
        
4. **If any list remains**, attach it to the merged list.
    

---

## **🔹 Java Code (Iterative Approach)**

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

public class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        // Dummy node to simplify edge cases
        ListNode dummy = new ListNode(-1);
        ListNode newListTail = dummy;

        // Traverse both lists
        while (list1 != null && list2 != null) {
            if (list1.val < list2.val) {
                newListTail.next = list1;
                list1 = list1.next;
            } else {
                newListTail.next = list2;
                list2 = list2.next;
            }
            newListTail = newListTail.next; // Move tail forward
        }

        // Attach the remaining nodes
        if (list1 != null) newListTail.next = list1;
        if (list2 != null) newListTail.next = list2;

        return dummy.next; // Return merged list, skipping dummy node
    }
}
```

---

## **🔹 Dry Run**

### **Example:**

```plaintext
list1 = [1 → 2 → 4]
list2 = [1 → 3 → 4]
```

### **Step-by-Step Execution:**

|Step|list1 (p1)|list2 (p2)|Merged List|
|---|---|---|---|
|1|**1** → 2 → 4|**1** → 3 → 4|`1` (from list2)|
|2|**1** → 2 → 4|3 → 4|`1 → 1` (from list1)|
|3|2 → 4|**3** → 4|`1 → 1 → 2` (from list1)|
|4|**4**|3 → 4|`1 → 1 → 2 → 3` (from list2)|
|5|**4**|**4**|`1 → 1 → 2 → 3 → 4` (from list1)|
|6|`null`|**4**|`1 → 1 → 2 → 3 → 4 → 4` (from list2)|

### **Final Merged List:**

```plaintext
1 → 1 → 2 → 3 → 4 → 4
```

---

## **🔹 Recursive Approach**

1. **Base Case:** If either list is `null`, return the other list.
    
2. **Recursive Step:**
    
    - Compare `list1.val` and `list2.val`.
        
    - The smaller node becomes the head.
        
    - Recursively merge the rest of the lists.
        

### **🔹 Java Code (Recursive)**

```java
public class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        if (list1 == null) return list2;
        if (list2 == null) return list1;

        if (list1.val < list2.val) {
            list1.next = mergeTwoLists(list1.next, list2);
            return list1;
        } else {
            list2.next = mergeTwoLists(list1, list2.next);
            return list2;
        }
    }
}
```

---

## **🔹 Time & Space Complexity**

|Approach|Time Complexity|Space Complexity|
|---|---|---|
|**Iterative**|`O(M + N)` (Traverse both lists once)|`O(1)` (Constant extra space)|
|**Recursive**|`O(M + N)`|`O(M + N)` (Recursive call stack)|

---

## **🔹 Why This Works**

✅ **Two-pointer approach ensures minimal comparisons**  
✅ **Dummy node simplifies merging without special cases**  
✅ **Recursive approach is elegant but may cause stack overflow for large inputs**

Would you like a dry run for the recursive approach too? 🚀