Here are **full structured notes** for the classic **“Minimum Path Sum in Triangular Grid”** problem – starting from brute-force recursion and progressing all the way to space-optimized dynamic programming.

---

## 🟩 Problem: Minimum Path Sum in Triangle Grid

You're given a 2D list `triangle`, where each `triangle[i]` represents a row of the triangle. You start from the top and move to **adjacent** numbers in the next row. Find the **minimum path sum** from top to bottom.

### 🔹 Constraints:

- You can move to index `j` or `j+1` in the next row.
    
- Return the minimum total path sum.
    

---

### 🔸 Example Input

```text
triangle = [
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```

### 🔸 Output: `11`

### 🔸 Explanation: `2 + 3 + 5 + 1 = 11` (minimum among all possible paths)

---

## ✅ Step-by-Step Approaches

---

### 🔸 1. **Brute Force - Recursion (Top-Down)**

#### ▶️ Idea:

From a cell (i,j), explore:

- Down → (i+1, j)
    
- Diagonal → (i+1, j+1)
    

```java
int minimumPathSum(int i, int j, List<List<Integer>> triangle) {
    if (i == triangle.size() - 1) {
        return triangle.get(i).get(j); // Base: bottom row
    }

    int down = triangle.get(i).get(j) + minimumPathSum(i + 1, j, triangle);
    int diagonal = triangle.get(i).get(j) + minimumPathSum(i + 1, j + 1, triangle);

    return Math.min(down, diagonal);
}
```

#### ⏱ Time: `O(2^n)`

#### 💾 Space: `O(n)` (recursion stack)

---

### 🔸 2. **Memoization (Top-Down DP)**

#### ▶️ Optimization:

Use a `dp[i][j]` table to store results of subproblems.

```java
int minimumPathSum(int i, int j, List<List<Integer>> triangle, int[][] dp) {
    if (i == triangle.size() - 1) return triangle.get(i).get(j);
    if (dp[i][j] != -1) return dp[i][j];

    int down = triangle.get(i).get(j) + minimumPathSum(i + 1, j, triangle, dp);
    int diag = triangle.get(i).get(j) + minimumPathSum(i + 1, j + 1, triangle, dp);

    return dp[i][j] = Math.min(down, diag);
}
```

#### ⏱ Time: `O(n^2)`

#### 💾 Space: `O(n^2)` + recursion stack

---

### 🔸 3. **Tabulation (Bottom-Up DP)**

#### ▶️ Idea:

Start from the last row and build the `dp` table upwards.

```java
int minimumTotal(List<List<Integer>> triangle) {
    int n = triangle.size();
    int[][] dp = new int[n][n];

    // Fill last row
    for (int j = 0; j < n; j++) {
        dp[n - 1][j] = triangle.get(n - 1).get(j);
    }

    // Fill from bottom to top
    for (int i = n - 2; i >= 0; i--) {
        for (int j = 0; j <= i; j++) {
            int down = dp[i + 1][j];
            int diag = dp[i + 1][j + 1];
            dp[i][j] = triangle.get(i).get(j) + Math.min(down, diag);
        }
    }

    return dp[0][0];
}
```

#### ⏱ Time: `O(n^2)`

#### 💾 Space: `O(n^2)`

---

### 🔸 4. **Space Optimized DP**

#### ▶️ Idea:

We only need the **next row** at a time, so use two 1D arrays.

```java
int minimumTotal(List<List<Integer>> triangle) {
    int n = triangle.size();
    int[] front = new int[n];

    // Fill base case
    for (int j = 0; j < n; j++) {
        front[j] = triangle.get(n - 1).get(j);
    }

    // Iterate from second last row to top
    for (int i = n - 2; i >= 0; i--) {
        int[] curr = new int[n];
        for (int j = 0; j <= i; j++) {
            int down = front[j];
            int diag = front[j + 1];
            curr[j] = triangle.get(i).get(j) + Math.min(down, diag);
        }
        front = curr;
    }

    return front[0];
}
```

#### ⏱ Time: `O(n^2)`

#### 💾 Space: `O(n)`

---

## 🧠 Intuition Recap:

At each cell, you have **only two options**: go down or diagonal.  
By recursively (or iteratively) exploring both and choosing the **minimum**, you build up the optimal result.

---

## ✅ Final Summary

|Approach|Time Complexity|Space Complexity|Notes|
|---|---|---|---|
|Recursion|O(2^n)|O(n)|Exponential, not efficient|
|Memoization|O(n²)|O(n²)|Top-down DP with cache|
|Tabulation|O(n²)|O(n²)|Bottom-up DP table|
|Space Optimized|O(n²)|O(n)|Only use 2 rows at a time|

---

Let me know if you'd like the **maximum path variant**, or **path reconstruction** version as well.