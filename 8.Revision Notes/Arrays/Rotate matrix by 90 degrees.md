Here’s the full DSA breakdown of the **“Rotate a Matrix by 90 Degrees Clockwise”** problem – covering **brute force to optimal**, with **Java code**, **intuition**, and **step-by-step dry run**.

---

# ✅ Problem: Rotate Matrix 90 Degrees (Clockwise)

---

## 🔹 Problem Statement

> Given an `n x n` 2D matrix, **rotate the matrix in-place by 90 degrees clockwise**.

---

### 🔸 Example:

```text
Input:
[
 [1,2,3],
 [4,5,6],
 [7,8,9]
]

Output:
[
 [7,4,1],
 [8,5,2],
 [9,6,3]
]
```

---

## ✅ Constraints

- Must do it **in-place** (i.e., modify original matrix)
    
- Matrix is **square** (n × n)
    

---

## 🔁 Pattern

- Matrix transformation
    
- Transpose + reverse
    
- In-place two-step swap
    

---

# 🔻 Approach 1: Extra Matrix (Brute Force)

### ✅ Java Code:

```java
public void rotate(int[][] matrix) {
    int n = matrix.length;
    int[][] rotated = new int[n][n];

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            rotated[j][n - 1 - i] = matrix[i][j];
        }
    }

    // Copy rotated into original
    for (int i = 0; i < n; i++) {
        System.arraycopy(rotated[i], 0, matrix[i], 0, n);
    }
}
```

---

### ⏱ Time & Space:

- Time: `O(n^2)`
    
- Space: `O(n^2)`
    
- ❌ Violates in-place constraint
    

---

# ✅ Approach 2: In-Place – Transpose + Reverse Rows

### 🔸 Idea:

1. **Transpose** the matrix (convert rows to columns)
    
2. **Reverse each row** to get the rotated matrix
    

---

### ✅ Java Code:

```java
public void rotate(int[][] matrix) {
    int n = matrix.length;

    // Step 1: Transpose (swap across the diagonal)
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            int temp = matrix[i][j];
            matrix[i][j] = matrix[j][i];
            matrix[j][i] = temp;
        }
    }

    // Step 2: Reverse each row
    for (int i = 0; i < n; i++) {
        reverseRow(matrix[i]);
    }
}

private void reverseRow(int[] row) {
    int left = 0, right = row.length - 1;
    while (left < right) {
        int temp = row[left];
        row[left] = row[right];
        row[right] = temp;
        left++;
        right--;
    }
}
```

---

### ⏱ Time & Space:

- Time: `O(n^2)`
    
- Space: `O(1)` ✅ In-place
    

---

## 🔁 Dry Run: 3×3 Matrix

### Input:

```
1 2 3  
4 5 6  
7 8 9
```

### Step 1 – Transpose:

```
1 4 7  
2 5 8  
3 6 9
```

### Step 2 – Reverse each row:

```
7 4 1  
8 5 2  
9 6 3 ✅
```

---

## 📊 Comparison Table

|Approach|Time|Space|In-Place|Notes|
|---|---|---|---|---|
|Extra Matrix (Brute Force)|O(n²)|O(n²)|❌|Easy, not allowed in interviews|
|Transpose + Reverse|O(n²)|O(1)|✅|Optimal and commonly asked method|

---

## 🔄 Bonus: Rotate Matrix 90° Counterclockwise

- **Transpose + reverse columns** instead of rows
    
- Or use the formula: `rotated[n-1-j][i] = matrix[i][j]`
    

---

## 🔗 Leetcode Link

- [Leetcode 48 – Rotate Image](https://leetcode.com/problems/rotate-image/)
    

---

## ✅ Summary

- This is a **must-know matrix manipulation** problem.
    
- Interviewers often look for the **in-place** solution.
    
- **Transpose + reverse rows** is the most optimal pattern.
    

---

Would you like:

- A reusable Java utility for rotating 90°, 180°, 270°?
    
- Problems that combine rotation with searching or transformation (like image manipulation or games)?