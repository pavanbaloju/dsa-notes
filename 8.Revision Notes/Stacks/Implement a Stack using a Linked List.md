### **✅ Implementing a Stack Using a Linked List in Java**

A **stack using a linked list** avoids the fixed-size limitation of an array-based stack. It dynamically allocates memory as needed.

---

### **🚀 Stack Operations**

1. **push(x)** → Insert an element at the top of the stack.
    
2. **pop()** → Remove and return the top element.
    
3. **peek() / top()** → Get the top element without removing it.
    
4. **isEmpty()** → Check if the stack is empty.
    

---

### **🔹 Java Implementation**

```java
// Node class for Linked List
class Node {
    int data;
    Node next;

    public Node(int data) {
        this.data = data;
        this.next = null;
    }
}

// Stack class using Linked List
class MyStack {

    private Node top; // Points to the top of the stack

    // Constructor
    public MyStack() {
        this.top = null; // Stack is initially empty
    }

    // Push an element onto the stack
    public void push(int x) {
        Node newNode = new Node(x);
        newNode.next = top; // New node points to the previous top
        top = newNode; // New node becomes the new top
    }

    // Pop the top element from the stack
    public int pop() {
        if (isEmpty()) {
            System.out.println("Stack Underflow! Cannot pop.");
            return -1;
        }
        int poppedValue = top.data;
        top = top.next; // Move top to the next node
        return poppedValue;
    }

    // Peek at the top element without removing it
    public int peek() {
        if (isEmpty()) {
            System.out.println("Stack is empty!");
            return -1;
        }
        return top.data;
    }

    // Check if stack is empty
    public boolean isEmpty() {
        return top == null;
    }
}

// Driver Code
public class Main {
    public static void main(String[] args) {
        MyStack stack = new MyStack();

        stack.push(10);
        stack.push(20);
        stack.push(30);
        System.out.println("Top element: " + stack.peek()); // Output: 30

        System.out.println("Popped: " + stack.pop()); // Output: 30
        System.out.println("Popped: " + stack.pop()); // Output: 20
        System.out.println("Is empty: " + stack.isEmpty()); // Output: false
    }
}
```

---

### **🛠 Explanation of Key Methods**

1. **`push(x)`**
    
    - Creates a new node with `x`.
        
    - Points `newNode.next` to the old `top`.
        
    - Updates `top` to `newNode`.
        
2. **`pop()`**
    
    - Checks if the stack is empty.
        
    - Stores `top.data`, moves `top` to `top.next`, and returns the stored value.
        
3. **`peek()`**
    
    - Returns `top.data` without modifying the stack.
        
4. **`isEmpty()`**
    
    - Returns `true` if `top == null`.
        

---

### **🔹 Time Complexity**

|Operation|Time Complexity|
|---|---|
|Push|**O(1)**|
|Pop|**O(1)**|
|Peek|**O(1)**|
|isEmpty|**O(1)**|

---

### **🚀 Key Takeaways**

- **Dynamic size**: No fixed array size limitation.
    
- **Efficient O(1) operations**: Insertions and deletions are constant time.
    
- **Uses extra memory** for storing `next` pointers in each node.
    

Would you like a **doubly linked list** stack for even faster traversal? 🚀