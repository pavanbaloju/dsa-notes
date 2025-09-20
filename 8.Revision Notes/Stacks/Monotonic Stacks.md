# **Monotonic Stacks: In-Depth Explanation**

## **1. Definition**

A **Monotonic Stack** is a **specialized stack** that maintains elements in either **increasing** or **decreasing** order. It is commonly used to solve **next greater, next smaller, and histogram-related problems** in **O(n)** time complexity.

### **Types of Monotonic Stacks**

1. **Monotonic Increasing Stack** (for finding next smaller elements)
    
    - Maintains elements in **increasing** order (smallest at the bottom, largest at the top).
    - Before pushing a new element, **pop all larger elements** since they are no longer needed.
    - Used for **next smaller element, previous smaller element** problems.
2. **Monotonic Decreasing Stack** (for finding next greater elements)
    
    - Maintains elements in **decreasing** order (largest at the bottom, smallest at the top).
    - Before pushing a new element, **pop all smaller elements** since they are no longer needed.
    - Used for **next greater element, previous greater element** problems.

---

## **2. How to Build a Monotonic Stack**

We use a **stack** and process elements **one by one**, popping unnecessary elements before inserting a new one.

### **Building a Monotonic Increasing Stack (For Next Smaller Element)**

```java
import java.util.*;

public class MonotonicIncreasingStack {
    public static int[] nextSmallerElement(int[] arr) {
        Stack<Integer> stack = new Stack<>();
        int[] result = new int[arr.length];
        Arrays.fill(result, -1);

        for (int i = arr.length - 1; i >= 0; i--) {
            // Pop larger elements
            while (!stack.isEmpty() && stack.peek() >= arr[i]) {
                stack.pop();
            }

            // Top of stack is the next smaller element
            if (!stack.isEmpty()) {
                result[i] = stack.peek();
            }

            stack.push(arr[i]);
        }

        return result;
    }
}
```

✅ **Front of the stack always holds the next smaller element**.

---

### **Building a Monotonic Decreasing Stack (For Next Greater Element)**

```java
import java.util.*;

public class MonotonicDecreasingStack {
    public static int[] nextGreaterElement(int[] arr) {
        Stack<Integer> stack = new Stack<>();
        int[] result = new int[arr.length];
        Arrays.fill(result, -1);

        for (int i = arr.length - 1; i >= 0; i--) {
            // Pop smaller elements
            while (!stack.isEmpty() && stack.peek() <= arr[i]) {
                stack.pop();
            }

            // Top of stack is the next greater element
            if (!stack.isEmpty()) {
                result[i] = stack.peek();
            }

            stack.push(arr[i]);
        }

        return result;
    }
}
```

✅ **Front of the stack always holds the next greater element**.

---

## **3. Use Cases of Monotonic Stacks**

### **(A) Next Greater Element (NGE)**

- **Problem:** Find the **next greater element** for each element in an array.
- **Why Monotonic Stack?** The stack maintains **decreasing order**, allowing `O(n)` lookup.

#### **Next Greater Element Using Monotonic Stack**

```java
public static int[] nextGreaterElement(int[] arr) {
    Stack<Integer> stack = new Stack<>();
    int[] result = new int[arr.length];
    Arrays.fill(result, -1);

    for (int i = arr.length - 1; i >= 0; i--) {
        while (!stack.isEmpty() && stack.peek() <= arr[i]) {
            stack.pop();
        }

        if (!stack.isEmpty()) {
            result[i] = stack.peek();
        }

        stack.push(arr[i]);
    }

    return result;
}
```

✅ **Time Complexity:** **O(n)**.

---

### **(B) Largest Rectangle in Histogram**

- **Problem:** Given an array representing heights of histogram bars, find the **largest rectangular area**.
- **Why Monotonic Stack?** It helps efficiently determine **left and right boundaries** for each bar.

#### **Histogram Largest Rectangle Area (Monotonic Stack)**

```java
public static int largestRectangleArea(int[] heights) {
    Stack<Integer> stack = new Stack<>();
    int maxArea = 0;
    int n = heights.length;

    for (int i = 0; i <= n; i++) {
        int h = (i == n) ? 0 : heights[i];

        while (!stack.isEmpty() && h < heights[stack.peek()]) {
            int height = heights[stack.pop()];
            int width = stack.isEmpty() ? i : i - stack.peek() - 1;
            maxArea = Math.max(maxArea, height * width);
        }

        stack.push(i);
    }

    return maxArea;
}
```

✅ **Efficient O(n) approach** instead of brute force O(n²).

---

### **(C) Trapping Rain Water**

- **Problem:** Given an elevation map, calculate **how much water it can trap**.
- **Why Monotonic Stack?** Helps track left and right boundaries for each bar.

#### **Trapping Rain Water Using Monotonic Stack**

```java
public static int trapRainWater(int[] height) {
    Stack<Integer> stack = new Stack<>();
    int water = 0;

    for (int i = 0; i < height.length; i++) {
        while (!stack.isEmpty() && height[i] > height[stack.peek()]) {
            int bottom = stack.pop();
            if (stack.isEmpty()) break;

            int width = i - stack.peek() - 1;
            int heightDiff = Math.min(height[i], height[stack.peek()]) - height[bottom];
            water += width * heightDiff;
        }

        stack.push(i);
    }

    return water;
}
```

✅ **Efficient O(n) approach for water trapping.**

---

### **(D) Stock Span Problem**

- **Problem:** Given daily stock prices, find **how many consecutive days the price was less than or equal** to today’s price.
- **Why Monotonic Stack?** Tracks **previous smaller** values efficiently.

#### **Stock Span Using Monotonic Stack**

```java
public static int[] stockSpan(int[] prices) {
    Stack<Integer> stack = new Stack<>();
    int[] span = new int[prices.length];

    for (int i = 0; i < prices.length; i++) {
        while (!stack.isEmpty() && prices[stack.peek()] <= prices[i]) {
            stack.pop();
        }

        span[i] = stack.isEmpty() ? (i + 1) : (i - stack.peek());

        stack.push(i);
    }

    return span;
}
```

✅ **O(n) solution for stock span calculation**.

---

## **4. Advantages of Monotonic Stack**

|**Advantage**|**Why?**|
|---|---|
|**O(1) Min/Max Retrieval**|The top of the stack always stores the next min/max.|
|**O(n) Complexity**|Each element is pushed and popped at most once.|
|**Avoids Sorting or Extra Data Structures**|More efficient than brute force approaches.|
|**Great for Histogram, Stock Prices, and Next Greater Problems**|Provides an optimal solution with minimal extra space.|

---

## **5. Summary & Takeaways**

✅ **Monotonic Stack maintains elements in increasing or decreasing order using a stack.**  
✅ **Used in Next Greater Element, Histogram Problems, Trapping Rain Water, Stock Span, etc.**  
✅ **Efficient O(n) alternative to brute-force O(n²) solutions.**  
✅ **Great for problems involving left/right boundaries, consecutive constraints, or range-based queries.**

Would you like more practice problems or further clarifications? Let me know!