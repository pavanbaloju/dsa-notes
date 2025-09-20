Here are **full notes** on solving **Minimum Path Sum in a Grid** (Leetcode 64) using all DP approaches: brute force recursion, memoization, tabulation, and space optimization.

---

### ✅ Problem: [Minimum Path Sum – Leetcode 64]

Given an `m x n` grid filled with **non-negative integers**, find a path from **top-left** to **bottom-right**, which **minimizes the sum** of all numbers along its path.  
You can **only move down or right** at any point in time.

---

## 1. 🧠 Problem Understanding

You're at `(0, 0)` and want to reach `(m-1, n-1)` with the **minimum sum**.  
At every step, you can either go **right** or **down**.

This is a variation of grid-based dynamic programming where:

- Each cell contributes to path cost
    
- Your goal is to **minimize** total cost
    

---

## 2. 🔁 Brute Force Recursion

### ▶️ Idea:

Try all possible paths from `(0, 0)` to `(m-1, n-1)` and choose the one with the minimum cost.

### ⛔ Base Case:

- If out of bounds → return `∞`
    
- If at `(0, 0)` → return `grid[0][0]`
    

### 🔁 Transition:

From `(i, j)`:

- Go **up**: `f(i-1, j)`
    
- Go **left**: `f(i, j-1)`
    

```java
int minPathSum(int i, int j, int[][] grid) {
    if (i < 0 || j < 0) return Integer.MAX_VALUE;
    if (i == 0 && j == 0) return grid[0][0];
    
    int up = minPathSum(i - 1, j, grid);
    int left = minPathSum(i, j - 1, grid);
    
    return grid[i][j] + Math.min(up, left);
}
```

### ❌ Time: `O(2^(m+n))` – Exponential

### ❌ Space: Recursion stack `O(m+n)`

---

## 3. 🧠 Memoization (Top-Down DP)

Use a `dp[i][j]` table to **store results** of subproblems.

```java
int dfs(int i, int j, int[][] grid, int[][] dp) {
    if (i < 0 || j < 0) return Integer.MAX_VALUE;
    if (i == 0 && j == 0) return grid[0][0];
    if (dp[i][j] != -1) return dp[i][j];

    int up = dfs(i - 1, j, grid, dp);
    int left = dfs(i, j - 1, grid, dp);

    return dp[i][j] = grid[i][j] + Math.min(up, left);
}
```

In the main function:

```java
public int minPathSum(int[][] grid) {
    int m = grid.length, n = grid[0].length;
    int[][] dp = new int[m][n];
    for (int[] row : dp) Arrays.fill(row, -1);
    return dfs(m - 1, n - 1, grid, dp);
}
```

### ✅ Time: `O(m*n)`

### ✅ Space: `O(m*n)` + Recursion stack

---

## 4. 🔽 Tabulation (Bottom-Up DP)

Start from `(0, 0)` and fill the `dp` table until `(m-1, n-1)`.

```java
public int minPathSum(int[][] grid) {
    int m = grid.length, n = grid[0].length;
    int[][] dp = new int[m][n];

    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (i == 0 && j == 0)
                dp[i][j] = grid[i][j];
            else {
                int up = i > 0 ? dp[i - 1][j] : Integer.MAX_VALUE;
                int left = j > 0 ? dp[i][j - 1] : Integer.MAX_VALUE;
                dp[i][j] = grid[i][j] + Math.min(up, left);
            }
        }
    }

    return dp[m - 1][n - 1];
}
```

### ✅ Time: `O(m*n)`

### ✅ Space: `O(m*n)`

---

## 5. 💾 Space Optimized DP

You only need the **previous row** to compute current row → use 1D arrays.

```java
public int minPathSum(int[][] grid) {
    int m = grid.length, n = grid[0].length;
    int[] prev = new int[n];

    for (int i = 0; i < m; i++) {
        int[] curr = new int[n];
        for (int j = 0; j < n; j++) {
            if (i == 0 && j == 0) {
                curr[j] = grid[i][j];
            } else {
                int up = i > 0 ? prev[j] : Integer.MAX_VALUE;
                int left = j > 0 ? curr[j - 1] : Integer.MAX_VALUE;
                curr[j] = grid[i][j] + Math.min(up, left);
            }
        }
        prev = curr;
    }

    return prev[n - 1];
}
```

### ✅ Time: `O(m*n)`

### ✅ Space: `O(n)`

---

## 🔍 Edge Cases

- Grid has only 1 row or 1 column → solution is sum of that row/column
    
- Very large grid → prefer space optimized version
    

---

## ✅ Summary of Approaches

|Approach|Time|Space|
|---|---|---|
|Brute Recursion|`O(2^n)`|`O(n)`|
|Memoization (Top)|`O(m*n)`|`O(m*n)`|
|Tabulation (Bottom)|`O(m*n)`|`O(m*n)`|
|Space Optimized|`O(m*n)`|`O(n)`|

---

## 📌 Related Problems

- Unique Paths I (Leetcode 62)
    
- Unique Paths II (Leetcode 63)
    
- Minimum Falling Path Sum (Leetcode 931)
    
- Dungeon Game (Leetcode 174)
    
- Minimum Cost to Make at Least One Valid Path in a Grid (Leetcode 1368)
    

---

Let me know if you want:

- Full trace of how the DP table is filled
    
- Code to reconstruct the path that gave the minimum sum
    
- A dry run example on a specific input