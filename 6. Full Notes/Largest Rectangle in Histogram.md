## **Largest Rectangle in Histogram - Monotonic Stack Approach**

### **📌 Problem Statement**

Given an array `heights[]` representing the histogram's bar heights where the width of each bar is **1**, return the **area of the largest rectangle** in the histogram.

---

## **🔹 Approach: Using Monotonic Increasing Stack**

### **📌 Key Observations**

- A **rectangle's width extends** until we hit a **shorter bar**.
    
- We need to efficiently find:
    
    1. **Previous Smaller Element (PSE)** → Left boundary of rectangle.
        
    2. **Next Smaller Element (NSE)** → Right boundary of rectangle.
        
- **Using a Monotonic Increasing Stack**:
    
    - The stack stores **indices** of histogram bars in increasing order.
        
    - When a **shorter bar** is encountered, pop elements and compute areas.
        

---

## **🔹 Algorithm (Step-by-Step)**

1. **Initialize a stack (`stk`)** to store indices.
    
2. **Iterate through each bar (`i` from `0` to `n`)**:
    
    - While the **stack is not empty** and `heights[i] < heights[stk.peek()]`:
        
        - Pop the **top index (`j`)** from the stack.
            
        - Compute the **height** = `heights[j]`.
            
        - Compute the **width** = `i - stk.peek() - 1` (if stack is empty, width is `i`).
            
        - Update **max area**.
            
    - Push **current index `i`** onto the stack.
        
3. **Process remaining bars in stack**:
    
    - Compute area using width up to `n` since no NSE exists.
        
4. **Return `maxArea`**.
    

---

## **🔹 Dry Run**

### **Example Input:**

```java
heights = [2,1,5,6,2,3]
```

|Step|i|heights[i]|Stack (`stk`)|Popped Elements|Area Calculation|
|---|---|---|---|---|---|
|1|0|2|`[0]`|-|-|
|2|1|1|`[1]`|`0` (since `2 > 1`)|Area = `2 × 1 = 2`|
|3|2|5|`[1,2]`|-|-|
|4|3|6|`[1,2,3]`|-|-|
|5|4|2|`[1,4]`|`3` (Area = `6 × 1 = 6`), `2` (Area = `5 × 2 = 10`)|`maxArea = 10`|
|6|5|3|`[1,4,5]`|-|-|
|7|End|-|Process remaining|`5` (Area = `3 × 1 = 3`), `4` (Area = `2 × 4 = 8`)|`maxArea = 10`|

### **Final `maxArea`:**

```
10
```

---

## **🔹 Java Code**

```java
import java.util.*;

class Solution {
    public int largestRectangleArea(int[] heights) {
        int n = heights.length;
        Stack<Integer> stk = new Stack<>();
        int maxArea = 0;

        for (int i = 0; i <= n; i++) {
            int currHeight = (i == n) ? 0 : heights[i]; // Append 0 at the end for final processing so that elements with no NSE would be popped and area is calculatede

            // Maintain a monotonic increasing stack
            while (!stk.isEmpty() && currHeight < heights[stk.peek()]) {
                int h = heights[stk.pop()]; // Pop top element (NSE)
                int width = stk.isEmpty() ? i : i - stk.peek() - 1; // Compute width (PSE)
                maxArea = Math.max(maxArea, h * width); // Update max area
            }
            
            stk.push(i); // Push current index
        }

        return maxArea;
    }
}
```

---

## **🔹 Complexity Analysis**

- **Time Complexity:** **O(n)**
    
    - Each element is pushed **once** and popped **once** → **O(n) total**.
        
- **Space Complexity:** **O(n)** (Stack stores indices in the worst case).
    

---

## **🔹 Summary**

|**Concept**|**Explanation**|
|---|---|
|**Stack Type**|**Monotonic Increasing Stack (stores indices)**|
|**When do we pop?**|If `heights[i] < heights[stk.peek()]` (i.e., found next smaller)|
|**What happens after popping?**|Compute area using `h * width`|
|**What if stack is empty?**|Use `width = i`|
|**Time Complexity**|**O(n)** (Each element pushed & popped at most once)|
|**Space Complexity**|**O(n)** (Stack stores indices)|

This is the **optimal approach** using **monotonic stacks** for solving **Largest Rectangle in Histogram** efficiently. 🚀