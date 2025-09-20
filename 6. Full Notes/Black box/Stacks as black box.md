Here’s the **Black Box Learning Breakdown for Stacks**, now including **Monotonic Stacks**, with Java examples.

---

# **Stack – Black Box Learning Approach**

## **1. Input**

A **Stack** is a **Last-In, First-Out (LIFO)** data structure where elements are added and removed from the **top**.

- **Push:** Inserts an element at the top.
- **Pop:** Removes the top element.
- **Peek:** Returns the top element without removing it.

### **Stack Implementation in Java**

Using **Java’s Stack class**:

```java
import java.util.Stack;

Stack<Integer> stack = new Stack<>();
stack.push(10);
stack.push(20);
stack.push(30);
```

Using **Linked List (Custom Implementation)**:

```java
class Node {
    int data;
    Node next;
    Node(int data) { this.data = data; }
}

class StackLinkedList {
    Node top;
    
    void push(int data) {
        Node newNode = new Node(data);
        newNode.next = top;
        top = newNode;
    }
    
    int pop() {
        if (top == null) throw new RuntimeException("Stack Underflow");
        int val = top.data;
        top = top.next;
        return val;
    }
}
```

---

## **2. Output**

- **Top element retrieval (`peek()`).**
- **Elements removed in LIFO order (`pop()`).**
- **Stack can be empty after multiple pops.**

Example:

```java
System.out.println(stack.peek());  // Output: 30
stack.pop();
System.out.println(stack.peek());  // Output: 20
```

---

## **3. Operations**

### **Basic Operations**

|Operation|Example (Java)|Best Case|Average Case|Worst Case|
|---|---|---|---|---|
|**Push (Insert at Top)**|`stack.push(x);`|**O(1)**|**O(1)**|**O(1)**|
|**Pop (Remove from Top)**|`stack.pop();`|**O(1)**|**O(1)**|**O(1)**|
|**Peek (View Top Element)**|`stack.peek();`|**O(1)**|**O(1)**|**O(1)**|
|**Search Element**|`stack.search(x);`|**O(1)** (top)|**O(n)**|**O(n)**|
|**Check If Empty**|`stack.isEmpty();`|**O(1)**|**O(1)**|**O(1)**|
|**Iterate Over Stack**|`for (int x : stack)`|**O(n)**|**O(n)**|**O(n)**|

---

## **4. Monotonic Stacks**

A **Monotonic Stack** is a stack that maintains elements in a specific order (increasing or decreasing).

- Used for **range queries**, **next greater/smaller element**, and **stock span problems**.
- Two types:
    - **Monotonically Increasing Stack:** Maintains elements in **ascending order**.
    - **Monotonically Decreasing Stack:** Maintains elements in **descending order**.

### **Example: Next Greater Element (Monotonic Decreasing Stack)**

```java
import java.util.Stack;

public class NextGreaterElement {
    public static int[] nextGreater(int[] arr) {
        int n = arr.length;
        int[] result = new int[n];
        Stack<Integer> stack = new Stack<>();

        for (int i = n - 1; i >= 0; i--) {
            while (!stack.isEmpty() && stack.peek() <= arr[i]) {
                stack.pop();
            }
            result[i] = stack.isEmpty() ? -1 : stack.peek();
            stack.push(arr[i]);
        }
        return result;
    }

    public static void main(String[] args) {
        int[] arr = {2, 1, 4, 3};
        int[] res = nextGreater(arr);
        for (int num : res) {
            System.out.print(num + " ");  // Output: 4 4 -1 -1
        }
    }
}
```

🔹 **Monotonic Stack ensures elements are processed efficiently in O(n) time complexity.**

---

## **5. Time and Space Complexities**

### **Time Complexity Summary**

|Operation|Best Case|Average Case|Worst Case|
|---|---|---|---|
|**Push/Pop/Peek**|O(1)|O(1)|O(1)|
|**Search**|O(1) (top)|O(n)|O(n)|
|**Iterate Over Stack**|O(n)|O(n)|O(n)|
|**Monotonic Stack Operations**|O(1)|O(n)|O(n)|

### **Space Complexity**

- **O(n)** for storing `n` elements.

---

## **6. Use Cases**

- **Expression evaluation** (e.g., infix to postfix conversion).
- **Undo/Redo functionality** (text editors, web browser history).
- **Backtracking algorithms** (e.g., recursion, depth-first search).
- **Function call stack in programming languages.**
- **Balancing symbols (e.g., parenthesis matching).**
- **Monotonic Stacks for range queries** (e.g., next greater/smaller element, stock span).

---

## **7. Problems in this Pattern**

### **Easy**

- Implement Stack using Array or Linked List
- Reverse a String using Stack
- Check for Balanced Parentheses

### **Medium**

- Next Greater Element (Monotonic Stack)
- Implement Min Stack (Stack with Min Retrieval in O(1))
- Evaluate Postfix Expression

### **Hard**

- Largest Rectangle in Histogram (Monotonic Stack)
- Remove K Digits to Get Smallest Number
- Decode String (Nested String Expansion)

---

## **8. Explore - Other Related Concepts**

- **Queue (FIFO):** The opposite of a stack in behavior.
- **Deque (Double-ended queue):** Allows both stack and queue operations.
- **Recursion & Call Stack:** Function calls in programming use a stack.
- **Monotonic Stacks:** Optimized for problems involving "next greater" or "next smaller" elements.

---

## **Conclusion**

By treating Stack as a **black box**, we:  
✅ **Observed how input changes affect output.**  
✅ **Identified patterns in operations.**  
✅ **Implemented solutions before diving into deep theory.**  
✅ **Introduced Monotonic Stacks for range query optimizations.**

Would you like to continue with **Queue, Deque, or Priority Queue (Heap) next?**