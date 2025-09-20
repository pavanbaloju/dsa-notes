Here's a complete DSA note on the classic matrix traversal problem: **“Print Matrix in Spiral Order”** — covering **logic**, **Java code**, **dry run**, and **variations**.

---

# ✅ Problem: Print Matrix in Spiral Order

(aka **Spiral Matrix** – Leetcode 54)

---

## 🔹 Problem Statement

> Given an `m x n` matrix, return all elements of the matrix in **spiral order**.

---

### 🔸 Example:

```text
Input:
[
 [1, 2, 3],
 [4, 5, 6],
 [7, 8, 9]
]

Output: [1, 2, 3, 6, 9, 8, 7, 4, 5]
```

---

## 🔁 Pattern: **Layer-by-Layer traversal using 4 pointers**

We use:

- `top` – starting row
    
- `bottom` – ending row
    
- `left` – starting column
    
- `right` – ending column
    

---

## ✅ Spiral Traversal Algorithm (Clockwise)

1. Traverse top row → `left → right`
    
2. Traverse right column ↓ `top → bottom`
    
3. Traverse bottom row ← `right → left` (only if `top <= bottom`)
    
4. Traverse left column ↑ `bottom → top` (only if `left <= right`)
    
5. Shrink boundaries inward
    

---

## ✅ Java Code – Spiral Order

```java
public List<Integer> spiralOrder(int[][] matrix) {
    List<Integer> result = new ArrayList<>();

    if (matrix == null || matrix.length == 0) return result;

    int top = 0, bottom = matrix.length - 1;
    int left = 0, right = matrix[0].length - 1;

    while (top <= bottom && left <= right) {

        // Traverse top row
        for (int i = left; i <= right; i++) {
            result.add(matrix[top][i]);
        }
        top++;

        // Traverse right column
        for (int i = top; i <= bottom; i++) {
            result.add(matrix[i][right]);
        }
        right--;

        // Traverse bottom row
        if (top <= bottom) {
            for (int i = right; i >= left; i--) {
                result.add(matrix[bottom][i]);
            }
            bottom--;
        }

        // Traverse left column
        if (left <= right) {
            for (int i = bottom; i >= top; i--) {
                result.add(matrix[i][left]);
            }
            left++;
        }
    }

    return result;
}
```

---

## 🔁 Dry Run Example

### Input:

```text
[1, 2, 3]  
[4, 5, 6]  
[7, 8, 9]
```

### Output (Step-by-step):

```
→ 1, 2, 3  
↓ 6, 9  
← 8, 7  
↑ 4  
→ 5 ✅
```

---

## ⏱ Time and Space Complexity

|Metric|Value|
|---|---|
|Time|O(m × n)|
|Space|O(m × n) for output list|

---

## ⚠️ Edge Cases

- Empty matrix
    
- Single row or column
    
- Uneven dimensions (`2x3`, `3x2`, etc.)
    

---

## 📦 Variations

|Problem|Idea|
|---|---|
|Print reverse spiral|Traverse in reverse order|
|Print in spiral without extra space|Just print, don't store|
|Spiral matrix generation (LC 59)|Build matrix from 1 to n²|

---

## 🔗 Leetcode Links

- [Leetcode 54 – Spiral Matrix](https://leetcode.com/problems/spiral-matrix/)
    
- [Leetcode 59 – Spiral Matrix II](https://leetcode.com/problems/spiral-matrix-ii/)
    

---

## ✅ Summary

- Use **four pointers**: `top`, `bottom`, `left`, `right`
    
- Traverse **clockwise** while shrinking the bounds
    
- Be careful with **corner cases** (e.g., when only one row/column is left)
    

---

Would you like:

- A version that returns a string instead of a list?
    
- An in-place spiral traversal visualizer or dry run?
    
- A follow-up version that builds spiral matrix from 1 to n² (LC 59)? 