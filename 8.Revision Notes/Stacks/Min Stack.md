Here are multiple approaches to solving the **Min Stack** problem, with their pros and cons.

---

## **Approach 1️⃣: Using Two Stacks (Main Stack + Min Stack)**

**Idea:**

- Use two stacks:
    
    1. **`mainStack`** → Stores all values.
        
    2. **`minStack`** → Stores the **minimum value at each stage**.
        

**Operations:**

- `push(val)`: Push `val` into `mainStack`. If `minStack` is empty or `val ≤ minStack.peek()`, push `val` into `minStack`.
    
- `pop()`: If `mainStack.peek() == minStack.peek()`, pop from both stacks.
    
- `top()`: Return `mainStack.peek()`.
    
- `getMin()`: Return `minStack.peek()`.
    

**Code:**

```java
import java.util.Stack;

class MinStack {
    private Stack<Integer> mainStack;
    private Stack<Integer> minStack;

    public MinStack() {
        mainStack = new Stack<>();
        minStack = new Stack<>();
    }

    public void push(int val) {
        mainStack.push(val);
        if (minStack.isEmpty() || val <= minStack.peek()) {
            minStack.push(val);
        }
    }

    public void pop() {
        if (mainStack.isEmpty()) return;
        if (mainStack.peek().equals(minStack.peek())) {
            minStack.pop();
        }
        mainStack.pop();
    }

    public int top() {
        return mainStack.peek();
    }

    public int getMin() {
        return minStack.peek();
    }
}
```

✅ **Time Complexity:** O(1) for all operations.  
✅ **Space Complexity:** O(N) for `minStack` (in worst case).

**Pros:**

- Simple to implement.
    
- Efficient operations.
    

**Cons:**

- Uses extra space for `minStack`.
    

---

## **Approach 2️⃣: Using a Single Stack (Storing Min with Value)**

**Idea:**

- Instead of using two stacks, store **(value, currentMin)** as a **pair** in a single stack.
    

**Operations:**

- `push(val)`: Push **(val, minSoFar)** tuple.
    
- `pop()`: Pop the top tuple.
    
- `top()`: Return the first value of the top tuple.
    
- `getMin()`: Return the second value of the top tuple.
    

**Code:**

```java
import java.util.Stack;

class MinStack {
    private Stack<int[]> stack;

    public MinStack() {
        stack = new Stack<>();
    }

    public void push(int val) {
        int min = stack.isEmpty() ? val : Math.min(val, stack.peek()[1]);
        stack.push(new int[]{val, min});
    }

    public void pop() {
        stack.pop();
    }

    public int top() {
        return stack.peek()[0];
    }

    public int getMin() {
        return stack.peek()[1];
    }
}
```

✅ **Time Complexity:** O(1) for all operations.  
✅ **Space Complexity:** O(N) (same as the two-stack approach but optimized).

**Pros:**

- Only one stack is used instead of two.
    

**Cons:**

- Still requires O(N) extra space.
    

---

### **Approach 3️⃣: Using a Stack with Relative Minimum Difference**

This approach is a space-optimized solution that **does not require an additional stack** for tracking the minimum values. Instead, we store values **relative to the current minimum** to save space while maintaining constant-time operations.

---

## **Key Idea**

1. Instead of storing the actual values in the stack, we store **the difference between the current value and the minimum value**.
    
2. If the pushed value is smaller than the current `min`, we store a **negative encoded value** to indicate that `min` has changed.
    
3. When popping, if we detect a negative stored value, we **recover the previous minimum** before updating.
    

This ensures that `getMin()` always runs in **O(1) time** without extra space beyond the primary stack.

---

## **How the Stack Works**

Each value stored in the stack can be:

1. **A normal value (`val - min`)** → When `val ≥ min`
    
2. **A negative encoded value (`val - min`)** → When `val < min`, meaning `val` is the new minimum
    

Using this technique, we can keep track of the **minimum value efficiently without an auxiliary stack**.

---

## **Operations Breakdown**

### **Push Operation (`push(val)`)**

- If the stack is empty:
    
    - Store `0` and set `min = val` because `val` is the smallest so far.
        
- Otherwise:
    
    - If `val ≥ min`: Store `val - min` (normal positive difference).
        
    - If `val < min`: Store `(val - min)`, which is **negative**, and update `min = val`.
        

### **Pop Operation (`pop()`)**

- If the popped value is **negative**, this means `min` was updated when pushing this value.
    
    - We recover the previous `min` using:
        
        ```
        min = min - poppedValue
        ```
        
- Otherwise, simply pop the value.
    

### **Top Operation (`top()`)**

- If the top value is **negative**, return `min` (since it was the new minimum).
    
- Otherwise, return `min + stack.peek()`.
    

### **Get Minimum (`getMin()`)**

- Directly return `min`.
    

---

## **Code Implementation**

```java
import java.util.Stack;

class MinStack {
    private Stack<Long> stack; // Stack to store the values
    private long min; // Tracks the minimum element

    public MinStack() {
        stack = new Stack<>();
    }

    public void push(int val) {
        if (stack.isEmpty()) {
            min = val;
            stack.push(0L);  // Store 0 as the difference (since val = min)
        } else {
            long diff = (long) val - min;
            stack.push(diff);
            if (val < min) { // If val is smaller, update min
                min = val;
            }
        }
    }

    public void pop() {
        if (stack.isEmpty()) return;
        long top = stack.pop();
        if (top < 0) { // Negative value indicates min was updated
            min = min - top; // Recover previous min
        }
    }

    public int top() {
        long top = stack.peek();
        return (top < 0) ? (int) min : (int) (top + min);
    }

    public int getMin() {
        return (int) min;
    }
}
```

---

## **Dry Run Example**

### **Example: Push(3), Push(5), Push(2), Push(1), Pop(), GetMin()**

We will track:

- `stack` contents
    
- `min` updates
    

|Operation|Stack (Stored Values)|Min|Explanation|
|---|---|---|---|
|push(3)|`0`|3|First element, store `0`, min = 3|
|push(5)|`0, 2`|3|Store `5-3=2` (min unchanged)|
|push(2)|`0, 2, -1`|2|`2 < 3`, store `2-3=-1`, update min = 2|
|push(1)|`0, 2, -1, -1`|1|`1 < 2`, store `1-2=-1`, update min = 1|
|pop()|`0, 2, -1`|2|Popped `-1`, recover min `2 - (-1) = 2`|
|getMin()|`0, 2, -1`|2|Returns current min = 2|

---

## **Why This Works?**

1. We use the **difference** between the new value and the current `min`, allowing us to encode information efficiently.
    
2. **Negative values** indicate `min` was updated, which allows us to **recover previous min values** when popping.
    
3. The `getMin()` operation always runs in **O(1) time**, since `min` is updated directly when pushing and popping.
    

---

## **Complexity Analysis**

|Operation|Time Complexity|Space Complexity|
|---|---|---|
|`push()`|**O(1)**|**O(1)**|
|`pop()`|**O(1)**|**O(1)**|
|`top()`|**O(1)**|**O(1)**|
|`getMin()`|**O(1)**|**O(1)**|

---

## **Pros and Cons**

✅ **Pros:**

- **Optimized Space Complexity:** O(1), using only a single stack.
    
- **O(1) Time Complexity:** All operations take constant time.
    
- **No Extra Stack Required:** Unlike the two-stack approach.
    

❌ **Cons:**

- **Slightly Complex Logic:** Requires understanding the encoding mechanism.
    
- **Negative Encoding Might Be Confusing:** Debugging may be harder.
    

---

## **When to Use This Approach?**

- When **space optimization is required**.
    
- When **you need O(1) time complexity** for all operations.
    
- If **debugging complexity is acceptable**.
    

Would you like a more **visual explanation** with pointer movements? 🚀