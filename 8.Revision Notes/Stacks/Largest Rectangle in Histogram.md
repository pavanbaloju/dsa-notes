Here's a **complete merged guide** for **Leetcode 84 – Largest Rectangle in Histogram**, covering all approaches step by step:

---

# 📘 Problem: Largest Rectangle in Histogram (Leetcode 84)

---

## ✅ Problem Statement

You are given an array `heights[]` representing the histogram bar heights.  
Return the **area of the largest rectangle** that can be formed from contiguous bars.

---

### 🔸 Example

```java
Input:  [2,1,5,6,2,3]
Output: 10
Explanation: The largest rectangle is formed by bars at index 2 and 3 with height 5 and 6 → area = 5 * 2 = 10
```

---

# 🛠️ Approach 1 – Brute Force (O(n²))

### 🔹 Idea

For each pair of indices `i` and `j`, compute the min height from `i` to `j` and calculate `area = height * width`.

### ✅ Java Code

```java
public int largestRectangleAreaBrute(int[] heights) {
    int maxArea = 0;
    int n = heights.length;

    for (int i = 0; i < n; i++) {
        int minHeight = heights[i];
        for (int j = i; j < n; j++) {
            minHeight = Math.min(minHeight, heights[j]);
            int width = j - i + 1;
            maxArea = Math.max(maxArea, minHeight * width);
        }
    }

    return maxArea;
}
```

### ⏱️ Time: O(n²)

### 📦 Space: O(1)

---

# ✅ Approach 2 – NSL + NSR (O(n))

### 🔹 Idea

For each bar:

- Extend rectangle to the **left** until a smaller bar
    
- Extend to the **right** until a smaller bar
    
- Width = `NSR[i] - NSL[i] - 1`
    
- Area = `heights[i] * width`
    

### 🔸 Helper Methods (NSL and NSR)

```java
private int[] pse(int[] heights) {
    int[] res = new int[heights.length];
    Stack<Integer> stack = new Stack<>();
    for (int i = 0; i < heights.length; i++) {
        while (!stack.isEmpty() && heights[stack.peek()] >= heights[i]) stack.pop();
        res[i] = stack.isEmpty() ? -1 : stack.peek();
        stack.push(i);
    }
    return res;
}

private int[] nse(int[] heights) {
    int[] res = new int[heights.length];
    Stack<Integer> stack = new Stack<>();
    int n = heights.length;
    for (int i = n - 1; i >= 0; i--) {
        while (!stack.isEmpty() && heights[stack.peek()] >= heights[i]) stack.pop();
        res[i] = stack.isEmpty() ? n : stack.peek();
        stack.push(i);
    }
    return res;
}
```

### 🔸 Final Method

```java
public int largestRectangleAreaNSLNSR(int[] heights) {
    int n = heights.length;
    int[] left = pse(heights);
    int[] right = nse(heights);
    int maxArea = 0;

    for (int i = 0; i < n; i++) {
        int width = right[i] - left[i] - 1;
        int area = heights[i] * width;
        maxArea = Math.max(maxArea, area);
    }

    return maxArea;
}
```

### ⏱️ Time: O(n)

### 📦 Space: O(n)

---

# 🚀 Approach 3 – Most Optimized (One-Pass Stack, O(n))

### 🔹 Idea

Use a **monotonic increasing stack** to compute area **on the fly** while traversing `heights[]` from **left to right**.  
We add a sentinel `0` at the end to flush out remaining bars.

### ✅ Java Code

```java
public int largestRectangleArea(int[] heights) {
    Stack<Integer> stack = new Stack<>();
    int maxArea = 0;
    int n = heights.length;

    for (int i = 0; i <= n; i++) {
        int currHeight = (i == n) ? 0 : heights[i];

        while (!stack.isEmpty() && currHeight < heights[stack.peek()]) {
            int height = heights[stack.pop()];
            int width = stack.isEmpty() ? i : i - stack.peek() - 1;
            maxArea = Math.max(maxArea, height * width);
        }

        stack.push(i);
    }

    return maxArea;
}
```

### ⏱️ Time: O(n)

### 📦 Space: O(n)

---

## 🔁 Dry Run on `[2, 1, 5, 6, 2, 3]`

Add a `0` sentinel at the end: `[2, 1, 5, 6, 2, 3, 0]`

Stack Trace:

```
i=0: push 0
i=1: 1 < 2 → pop 0 → area = 2*1 = 2, push 1
i=2: 5 > 1 → push 2
i=3: 6 > 5 → push 3
i=4: 2 < 6 → pop 3 → 6*1=6, pop 2 → 5*2=10, push 4
i=5: 3 > 2 → push 5
i=6: 0 < 3 → pop 5 → 3*1=3, pop 4 → 2*4=8, pop 1 → 1*6=6
```

✅ Max area = **10**

---

# 🧠 When to Use What?

|Approach|When to Use|
|---|---|
|Brute Force|For understanding or small inputs|
|NSL + NSR|For educational clarity|
|One-Pass Stack|✅ Best in interviews and production use|

---

## 📌 Summary

| Item           | Value                                   |
| -------------- | --------------------------------------- |
| Time (Optimal) | O(n)                                    |
| Space          | O(n)                                    |
| Stack Type     | Monotonic Increasing Stack              |
| Optimization   | One-pass, calculate area while scanning |
| Edge Handling  | Sentinel `0` to flush stack             |

---

Would you like this exported as:

- A **PDF cheat sheet**?
    
- A **Java utility class** with method names and Javadoc?
    
- A **Quarkus endpoint** or console app version for input/output?
    

Let me know — I can generate and package it for fast reference.