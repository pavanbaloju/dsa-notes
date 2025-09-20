Here are **full notes** on solving **Unique Paths II** (Leetcode 63) using dynamic programming, from brute force recursion to space-optimized approaches:

---

### ✅ Problem: [Unique Paths II – Leetcode 63]

You are given an `m x n` grid with obstacles. Return the number of **unique paths** from the top-left corner to the bottom-right corner, considering that:

- You can only move **right** or **down**
    
- A cell with value `1` is an obstacle, and `0` is a free cell
    

---

## 1. 🧠 **Understanding the Problem**

Each cell is either `0` (free) or `1` (blocked). We start at `(0, 0)` and must reach `(m-1, n-1)`, moving **only right or down** and **not stepping on any obstacle**.

So this is a variation of the standard **grid DP** problem where we skip invalid (obstacle) paths.

---

## 2. 🔁 Brute Force (Recursion)

### ▶️ Approach:

Try all paths from `(i, j)` to `(0, 0)` recursively, but return 0 if we hit an obstacle or go out of bounds.

### ⛔ Base Cases:

- If `(i, j)` is out of bounds → return 0
    
- If `(i, j)` is an obstacle → return 0
    
- If `(i == 0 && j == 0)` → return 1 (start point)
    

### 🔁 Transition:

We can reach `(i, j)` from:

- Top: `(i - 1, j)`
    
- Left: `(i, j - 1)`
    

```java
int countPaths(int i, int j, int[][] grid) {
    if (i < 0 || j < 0 || grid[i][j] == 1) return 0;
    if (i == 0 && j == 0) return 1;
    return countPaths(i - 1, j, grid) + countPaths(i, j - 1, grid);
}
```

### ❌ Time: `O(2^(m*n))` – Exponential

### ❌ Space: Recursion stack `O(m+n)`

---

## 3. 🧠 Memoization (Top-Down DP)

Store results in `dp[i][j]` to avoid recomputation.

```java
int dfs(int i, int j, int[][] grid, int[][] dp) {
    if (i < 0 || j < 0 || grid[i][j] == 1) return 0;
    if (i == 0 && j == 0) return 1;
    if (dp[i][j] != -1) return dp[i][j];

    int up = dfs(i - 1, j, grid, dp);
    int left = dfs(i, j - 1, grid, dp);

    return dp[i][j] = up + left;
}
```

### ✅ Time: `O(m*n)`

### ✅ Space: `O(m*n)` + Recursion stack

---

## 4. 🔽 Tabulation (Bottom-Up DP)

Build the `dp` table from `(0, 0)` to `(m-1, n-1)`

```java
public int uniquePathsWithObstacles(int[][] grid) {
    int m = grid.length, n = grid[0].length;
    int[][] dp = new int[m][n];

    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (grid[i][j] == 1) {
                dp[i][j] = 0;  // Obstacle
            } else if (i == 0 && j == 0) {
                dp[i][j] = 1;  // Start
            } else {
                int up = i > 0 ? dp[i - 1][j] : 0;
                int left = j > 0 ? dp[i][j - 1] : 0;
                dp[i][j] = up + left;
            }
        }
    }

    return dp[m - 1][n - 1];
}
```

### ✅ Time: `O(m*n)`

### ✅ Space: `O(m*n)`

---

## 5. 💾 Space Optimization

Only previous row and current row are needed → use 1D array

```java
public int uniquePathsWithObstacles(int[][] grid) {
    int m = grid.length, n = grid[0].length;
    int[] prev = new int[n];

    for (int i = 0; i < m; i++) {
        int[] curr = new int[n];
        for (int j = 0; j < n; j++) {
            if (grid[i][j] == 1) {
                curr[j] = 0;
            } else if (i == 0 && j == 0) {
                curr[j] = 1;
            } else {
                int up = i > 0 ? prev[j] : 0;
                int left = j > 0 ? curr[j - 1] : 0;
                curr[j] = up + left;
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

## 💡 Edge Cases to Handle

- Starting cell `(0, 0)` is an obstacle → return 0
    
- Ending cell `(m-1, n-1)` is an obstacle → result is 0 automatically
    

---

## ✅ Summary of Approaches

|Approach|Time|Space|
|---|---|---|
|Brute Recursion|`O(2^n)`|`O(n)`|
|Memoization (Top)|`O(m*n)`|`O(m*n)`|
|Tabulation (Bottom)|`O(m*n)`|`O(m*n)`|
|Space Optimized|`O(m*n)`|`O(n)`|

---

Let me know if you want:

- The **path(s)** printed
    
- Variations (diagonal moves, obstacles with weights, etc.)
    
- Follow-ups like **minimum path sum** or **knight paths**