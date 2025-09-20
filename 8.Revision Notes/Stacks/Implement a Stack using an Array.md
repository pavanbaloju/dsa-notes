Here’s a **simple implementation of a stack using an array in Java** with all essential operations:

- **push(x)** → Add element `x` to the top of the stack.
    
- **pop()** → Remove and return the top element of the stack.
    
- **peek() / top()** → Return the top element without removing it.
    
- **isEmpty()** → Check if the stack is empty.
    
- **isFull()** → Check if the stack is full.
    

---

### **✅ Java Implementation of Stack Using Array**

```java
class MyStack {
    private int[] arr;  // Array to store stack elements
    private int top;    // Index of the top element
    private int capacity; // Maximum capacity of the stack

    // Constructor to initialize the stack
    public MyStack(int size) {
        arr = new int[size];
        capacity = size;
        top = -1; // Stack is initially empty
    }

    // Push element onto the stack
    public void push(int x) {
        if (isFull()) {
            System.out.println("Stack Overflow! Cannot push " + x);
            return;
        }
        arr[++top] = x;
    }

    // Pop element from the stack
    public int pop() {
        if (isEmpty()) {
            System.out.println("Stack Underflow! Cannot pop.");
            return -1;
        }
        return arr[top--];
    }

    // Peek: Get the top element without removing it
    public int peek() {
        if (isEmpty()) {
            System.out.println("Stack is empty!");
            return -1;
        }
        return arr[top];
    }

    // Check if stack is empty
    public boolean isEmpty() {
        return top == -1;
    }

    // Check if stack is full
    public boolean isFull() {
        return top == capacity - 1;
    }

    // Get the size of the stack
    public int size() {
        return top + 1;
    }
}

// Driver Code
public class Main {
    public static void main(String[] args) {
        MyStack stack = new MyStack(5);

        stack.push(10);
        stack.push(20);
        stack.push(30);
        System.out.println("Top element: " + stack.peek()); // Output: 30

        System.out.println("Popped: " + stack.pop()); // Output: 30
        System.out.println("Stack size: " + stack.size()); // Output: 2
        System.out.println("Is empty: " + stack.isEmpty()); // Output: false
    }
}
```

---

### **🛠 Explanation of Key Methods**

1. **`push(x)`**
    
    - Increments `top` and inserts `x` at `arr[top]`.
        
    - Checks if stack is full before inserting.
        
2. **`pop()`**
    
    - Returns `arr[top]` and decrements `top`.
        
    - Checks if stack is empty before popping.
        
3. **`peek()`**
    
    - Returns `arr[top]` without modifying `top`.
        
4. **`isEmpty()`**
    
    - Returns `true` if `top == -1`.
        
5. **`isFull()`**
    
    - Returns `true` if `top == capacity - 1`.
        

---

### **🔹 Time Complexity**

|Operation|Time Complexity|
|---|---|
|Push|**O(1)**|
|Pop|**O(1)**|
|Peek|**O(1)**|
|isEmpty|**O(1)**|
|isFull|**O(1)**|

---

### **🚀 Key Takeaways**

- Uses a **fixed-size array** → Better for **memory efficiency**.
    
- Runs in **O(1) time** for all operations.
    
- **Stack Overflow** occurs if the stack is full.
    
- **Stack Underflow** occurs if the stack is empty.
    

Would you like a **dynamic array-based stack** where the size grows automatically? 🚀