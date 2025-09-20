Here’s the **Singly Linked List implementation using a dummy node** to simplify edge cases (like inserting at head or deleting the first node).

---

### **📌 Why Use a Dummy Node?**

1. **Avoids special cases**: Insertion and deletion at head become uniform.
    
2. **Simplifies code**: No need to check if `head` is `null` explicitly.
    
3. **Prevents bugs**: The dummy node is never deleted, reducing corner case errors.
    

---

### **📌 Java Implementation (Using Dummy Node)**

```java
class MyLinkedList {
    
    // Node structure
    private static class Node {
        int val;
        Node next;
        
        Node(int val) {
            this.val = val;
            this.next = null;
        }
    }

    private Node dummy; // Dummy node (always present)
    private int size;   // Keeps track of the size

    public MyLinkedList() {
        dummy = new Node(-1); // Dummy node with arbitrary value
        size = 0;
    }
    
    // Get the value at the given index
    public int get(int index) {
        if (index < 0 || index >= size) return -1; // Out of bounds

        Node temp = dummy.next; // Start from the first real node
        for (int i = 0; i < index; i++) {
            temp = temp.next;
        }
        return temp.val;
    }
    
    // Insert a new node at head
    public void addAtHead(int val) {
        addAtIndex(0, val);
    }
    
    // Insert a new node at tail
    public void addAtTail(int val) {
        addAtIndex(size, val);
    }
    
    // Insert a new node at a specific index
    public void addAtIndex(int index, int val) {
        if (index < 0 || index > size) return; // Invalid index

        Node prev = dummy; // Start from dummy node
        for (int i = 0; i < index; i++) {
            prev = prev.next;
        }

        Node newNode = new Node(val);
        newNode.next = prev.next;
        prev.next = newNode;

        size++;
    }
    
    // Delete a node at a specific index
    public void deleteAtIndex(int index) {
        if (index < 0 || index >= size) return; // Invalid index

        Node prev = dummy; // Start from dummy node
        for (int i = 0; i < index; i++) {
            prev = prev.next;
        }

        prev.next = prev.next.next; // Remove the node
        size--;
    }
    
    // Display the linked list (for debugging)
    public void display() {
        Node temp = dummy.next; // Skip dummy node
        while (temp != null) {
            System.out.print(temp.val + " -> ");
            temp = temp.next;
        }
        System.out.println("null");
    }

    public static void main(String[] args) {
        MyLinkedList list = new MyLinkedList();
        
        list.addAtHead(10);
        list.addAtTail(20);
        list.addAtTail(30);
        list.addAtIndex(1, 15); // Insert 15 at index 1
        
        System.out.println("Linked List:");
        list.display();

        System.out.println("Value at index 2: " + list.get(2));

        list.deleteAtIndex(1);
        System.out.println("After deleting index 1:");
        list.display();
    }
}
```

---

### **📌 How Does Dummy Node Help?**

1. **Insertion at head**
    
    - `addAtHead(val)` simply calls `addAtIndex(0, val)`.
        
    - We don’t need to check if `head` is `null`, as the dummy node always exists.
        
2. **Deletion at head**
    
    - `deleteAtIndex(0)` works normally because we always start from the dummy node.
        
3. **Simplified Traversal**
    
    - All operations start from `dummy`, avoiding extra conditions for `head`.
        

---

### **📌 Complexity Analysis**

|Operation|Time Complexity|Explanation|
|---|---|---|
|`get(index)`|**O(N)**|Traverses up to `index`|
|`addAtHead(val)`|**O(1)**|Always inserts after `dummy`|
|`addAtTail(val)`|**O(N)**|Traverses to the end|
|`addAtIndex(i, v)`|**O(N)**|Traverses to `i-1`th node|
|`deleteAtIndex(i)`|**O(N)**|Traverses to `i-1`th node|

---

### **📌 Sample Output**

```
Linked List:
10 -> 15 -> 20 -> 30 -> null
Value at index 2: 20
After deleting index 1:
10 -> 20 -> 30 -> null
```

---

### **📌 Key Takeaways**

✅ **Using a dummy node removes edge cases** like inserting/deleting at head.  
✅ **All operations are handled uniformly**, making the implementation **cleaner**.  
✅ **Commonly used in linked list problems** to simplify logic.

Let me know if you need modifications or explanations! 🚀