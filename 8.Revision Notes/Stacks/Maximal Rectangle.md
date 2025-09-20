Here are the **full notes** for **Leetcode 85 – Maximal Rectangle**, including brute-force intuition, histogram transformation, optimal solution using Monotonic Stacks, dry runs, complexities, and Java code templates.

---

# 📘 Leetcode 85 – Maximal Rectangle: Full Notes

---

## ✅ Problem Statement

> Given a 2D binary matrix of `'0'`s and `'1'`s, find the **area of the largest rectangle** containing only 1's and return its area.

---

## 🔍 Example

```txt
Input:
[
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]

Output: 6
```

---

## 🧠 Brute Force Approach (Conceptual Only)

- Try every pair of top and bottom rows.
    
- For each column, check if all entries between those rows are 1.
    
- Find max rectangle using width × height.
    

### ⏱ Time: O(rows² × cols)

### 📦 Space: O(1)

Too slow for large inputs → needs optimization.

---

# 🚀 Optimized Approach – Histogram + Monotonic Stack

---

## 🔸 Key Insight

- Transform each row into a **histogram**: each column represents a bar with height equal to the count of **consecutive 1s** above it (including current row).
    
- For each histogram row, compute **Largest Rectangle in Histogram** using Monotonic Stack (Leetcode 84).
    

---

## 🔁 Step-by-Step Execution

### Example Matrix:

```txt
[
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]
```

### Histogram Heights per Row:

```
Row 0: [1, 0, 1, 0, 0]
Row 1: [2, 0, 2, 1, 1]
Row 2: [3, 1, 3, 2, 2]
Row 3: [4, 0, 0, 3, 0]
```

Each row becomes a histogram. For each, apply the **Largest Rectangle in Histogram** logic.

---

## 🧱 Core Algorithm

1. Initialize an array `heights[]` of size `cols`, filled with 0.
    
2. For each row:
    
    - If matrix[row][col] == '1' → heights[col] += 1
        
    - Else → heights[col] = 0
        
3. Use a Monotonic Stack to compute largest rectangle in this histogram.
    

---

## ✅ Java Code – Maximal Rectangle

```java
public int maximalRectangle(char[][] matrix) {
    if (matrix == null || matrix.length == 0 || matrix[0].length == 0) return 0;

    int maxArea = 0;
    int cols = matrix[0].length;
    int[] heights = new int[cols];

    for (char[] row : matrix) {
        for (int i = 0; i < cols; i++) {
            heights[i] = row[i] == '1' ? heights[i] + 1 : 0;
        }
        maxArea = Math.max(maxArea, largestRectangleArea(heights));
    }

    return maxArea;
}
```

---

## ✅ Java Code – Largest Rectangle in Histogram (One Pass Optimized)

```java
private int largestRectangleArea(int[] heights) {
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

---

## 🧠 Stack Logic Recap

For each bar in the histogram:

- If current bar is **taller**, push its index.
    
- If current bar is **shorter**, it bounds previous bars → pop stack, compute area.
    
- Use a **sentinel bar of height 0** at the end to flush stack.
    

---

## ⏱ Time and Space Complexity

|Metric|Value|
|---|---|
|Time|O(rows × cols)|
|Space|O(cols) for histogram and stack|

---

## 🔗 Related Problems

|Problem|Technique|
|---|---|
|Leetcode 84|Largest Rectangle in Histogram|
|Leetcode 221|Maximal Square (DP approach)|
|Leetcode 85|Maximal Rectangle|
|Leetcode 42|Trapping Rain Water|

---

## 📌 Monotonic Stack Template

|Stack Use Case|Traverse|Condition|
|---|---|---|
|NSR (Nearest Smaller R)|R → L|while stack.peek() ≥ curr|
|NSL (Nearest Smaller L)|L → R|while stack.peek() ≥ curr|
|Largest Rectangle|L → R|Same stack; pop and compute on fly|

---

## 🔄 Dry Run Walkthrough (Example)

Given:

```txt
Row 2: ["1","1","1","1","1"]
→ Histogram: [3, 1, 3, 2, 2]
```

Stack trace (with 0-sentinel logic):

- i=0: push
    
- i=1: 1 < 3 → pop → area=3×1=3
    
- i=1: push
    
- i=2: 3 > 1 → push
    
- i=3: 2 < 3 → pop → area=3×1=3, then push
    
- i=4: 2 = 2 → pop → area=2×1=2, push
    
- i=5: 0 → flush stack: max area found = **6**
    

---

## ✅ Final Summary

|Topic|Summary|
|---|---|
|Core Idea|Convert rows to histograms|
|Max Rectangle|Use largest histogram logic per row|
|Optimized Stack|Monotonic increasing|
|Final Complexity|Time: O(R×C), Space: O(C)|
|Useful For|Rectangle-in-grid problems|

---

## ✅ Reusable Java Templates

- `maximalRectangle()` → Main function
    
- `largestRectangleArea()` → Utility for each row
    

---

Would you like:

- Dry run animation of one full matrix step-by-step?
    
- Add row/col tracking to return the actual rectangle's coordinates?
    
- Export to Notion, PDF, or Markdown?
    

Let me know — I can generate it!