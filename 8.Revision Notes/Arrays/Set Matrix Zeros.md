Here's a complete DSA breakdown for the classic matrix problem **“Set Matrix Zeroes”** – from brute force to optimal, with **Java code**, **space/time trade-offs**, and **interview patterns**.

---

# ✅ Problem: Set Matrix Zeroes (Leetcode 73)

---

## 🔹 Problem Statement

> Given an `m x n` matrix, if an element is `0`, set its **entire row and column to 0**.  
> Do it **in-place** if possible.

---

### 🔸 Example:

```txt
Input:
[
  [1,1,1],
  [1,0,1],
  [1,1,1]
]

Output:
[
  [1,0,1],
  [0,0,0],
  [1,0,1]
]
```

---

## ✅ Constraints

- Must be **in-place** if possible
    
- Do **not use extra space proportional to m × n**
    
- Optimize for space
    

---

## 🧠 Pattern

- **Matrix transformation**
    
- **Marker trick / state encoding**
    
- **Space optimization**
    

---

# 🔻 Brute Force: Use Marker Matrix

### ✅ Java Code:

```java
public void setZeroes(int[][] matrix) {
    int m = matrix.length, n = matrix[0].length;
    boolean[][] mark = new boolean[m][n];

    // Mark the positions to be zeroed
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (matrix[i][j] == 0) {
                for (int k = 0; k < m; k++) mark[k][j] = true;
                for (int k = 0; k < n; k++) mark[i][k] = true;
            }
        }
    }

    // Apply the markings
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (mark[i][j]) matrix[i][j] = 0;
        }
    }
}
```

### ⏱ Time & Space:

- Time: `O(m * n)`
    
- Space: `O(m * n)`
    
- ❌ Not space-efficient
    

---

# 🔸 Better: Use Row and Column Marker Arrays

### ✅ Java Code:

```java
public void setZeroes(int[][] matrix) {
    int m = matrix.length, n = matrix[0].length;
    boolean[] rows = new boolean[m];
    boolean[] cols = new boolean[n];

    // Mark rows and columns
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (matrix[i][j] == 0) {
                rows[i] = true;
                cols[j] = true;
            }
        }
    }

    // Set matrix[i][j] to 0 if its row or column is marked
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (rows[i] || cols[j]) {
                matrix[i][j] = 0;
            }
        }
    }
}
```

### ⏱ Time & Space:

- Time: `O(m * n)`
    
- Space: `O(m + n)`
    
- ✅ Better, but still uses extra space
    

---

# ✅ Optimal: In-Place Using First Row & Column as Markers

### 🔸 Idea:

- Use **first row and first column** as the space to mark which row/column to zero.
    
- Track separately if **first row or column themselves need to be zeroed**.
    

---

### ✅ Java Code:

```java
public void setZeroes(int[][] matrix) {
    int m = matrix.length, n = matrix[0].length;
    boolean firstRowZero = false;
    boolean firstColZero = false;

    // Check if first row has zero
    for (int j = 0; j < n; j++) {
        if (matrix[0][j] == 0) {
            firstRowZero = true;
            break;
        }
    }

    // Check if first column has zero
    for (int i = 0; i < m; i++) {
        if (matrix[i][0] == 0) {
            firstColZero = true;
            break;
        }
    }

    // Use first row and column as marker
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            if (matrix[i][j] == 0) {
                matrix[i][0] = 0;
                matrix[0][j] = 0;
            }
        }
    }

    // Set cells based on markers
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                matrix[i][j] = 0;
            }
        }
    }

    // Zero out first row if needed
    if (firstRowZero) {
        for (int j = 0; j < n; j++) matrix[0][j] = 0;
    }

    // Zero out first column if needed
    if (firstColZero) {
        for (int i = 0; i < m; i++) matrix[i][0] = 0;
    }
}
```

---

### ⏱ Time & Space:

- Time: `O(m * n)`
    
- Space: `O(1)` → truly in-place
    
- ✅ Optimal and interview-preferred
    

---

## 🔁 Dry Run (Conceptual):

For input:

```
[1, 1, 1]
[1, 0, 1]
[1, 1, 1]
```

Markers added:

```
[1, 0, 1]   // matrix[0][1] = 0 due to [1][1]
[0, 0, 1]   // matrix[1][0] = 0
[1, 1, 1]
```

Final matrix after processing:

```
[1, 0, 1]
[0, 0, 0]
[1, 0, 1]
```

---

## 📊 Comparison Table

|Approach|Time|Space|Interview-Ready|Notes|
|---|---|---|---|---|
|Extra Matrix|O(m * n)|O(m * n)|❌|Simple but inefficient|
|Row & Column Arrays|O(m * n)|O(m + n)|⚠️|Acceptable but not best|
|In-Place with Markers|O(m * n)|O(1)|✅✅|Most optimal, common interview Q|

---

## 🔗 Leetcode Link

- [Leetcode 73 – Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/)
    

---

## ✅ Summary

- This is a **classic matrix in-place problem**.
    
- **Most optimal** solution reuses **1st row/col as flag markers**.
    
- Understand how to **preserve information** while modifying in-place.
    

---

Would you like:

- Visual explanation of in-place marker strategy?
    
- A practice sheet on matrix transformation problems (rotate, transpose, flood fill, etc.)?