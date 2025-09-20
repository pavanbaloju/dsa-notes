Here are **full notes** for the **"Grid Unique Paths"** problem using the **reverse approach** (starting from bottom-right `(m-1, n-1)` and going up or left to `(0, 0)`):

---

# 🧭 Problem: Grid Unique Paths (Reversed Direction)

### ✅ Problem Statement

You are given a `m x n` grid. Your robot is at the **bottom-right cell** `(m-1, n-1)`.  
You can only move **up** or **left** at any point in time.

Return the number of unique paths from **(m-1, n-1) to (0, 0)**.

---

## 🔁 Allowed Moves (from destination to start):

- Up `(i-1, j)`
    
- Left `(i, j-1)`
    

---

## 🧠 Intuition (in Reverse)

- If you're at cell `(i, j)`, the total number of paths to reach `(0, 0)` is the sum of:
    
    - The number of ways to reach `(0, 0)` from **(i-1, j)** — i.e., **coming from above**
        
    - The number of ways to reach `(0, 0)` from **(i, j-1)** — i.e., **coming from left**
        
- Base case: Reached `(0, 0)` → only **1 path**.
    
- Out of bounds → **0 paths**.
    

---

## ✅ Step 1: Recursion (TLE for large inputs)

```java
public int uniquePathsRecursive(int i, int j) {
    if (i < 0 || j < 0) return 0;          // Out of grid
    if (i == 0 && j == 0) return 1;        // Reached start point

    int up = uniquePathsRecursive(i - 1, j);
    int left = uniquePathsRecursive(i, j - 1);
    
    return up + left;
}

// Call with:
int result = uniquePathsRecursive(m - 1, n - 1);
```

⏱️ **Time Complexity:** Exponential  
📦 **Space Complexity:** O(path depth) = O(m + n)

---

## ✅ Step 2: Top-Down DP (Memoization)

```java
public int uniquePathsMemo(int i, int j, int[][] dp) {
    if (i < 0 || j < 0) return 0;
    if (i == 0 && j == 0) return 1;
    if (dp[i][j] != -1) return dp[i][j];

    int up = uniquePathsMemo(i - 1, j, dp);
    int left = uniquePathsMemo(i, j - 1, dp);
    
    return dp[i][j] = up + left;
}

public int uniquePaths(int m, int n) {
    int[][] dp = new int[m][n];
    for (int[] row : dp) Arrays.fill(row, -1);

    return uniquePathsMemo(m - 1, n - 1, dp);
}
```

⏱️ **Time Complexity:** O(m × n)  
📦 **Space Complexity:** O(m × n) + O(path depth)

---

## ✅ Step 3: Bottom-Up DP (Tabulation)

Even though the recursion starts from the bottom-right, **tabulation** always builds up from base cases.  
So we fill the table from **(0, 0)** to **(m-1, n-1)**.

```java
public int uniquePaths(int m, int n) {
    int[][] dp = new int[m][n];

    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (i == 0 && j == 0) dp[i][j] = 1;  // base case
            else {
                int up = i > 0 ? dp[i - 1][j] : 0;
                int left = j > 0 ? dp[i][j - 1] : 0;
                dp[i][j] = up + left;
            }
        }
    }

    return dp[m - 1][n - 1];
}
```

⏱️ **Time Complexity:** O(m × n)  
📦 **Space Complexity:** O(m × n)

---

## ✅ Step 4: Space Optimized (1D Array)

We only need the **current row and previous row** (or just previous values in the row), so we can use 1D DP.

```java
public int uniquePaths(int m, int n) {
    int[] prev = new int[n];

    for (int i = 0; i < m; i++) {
        int[] cur = new int[n];
        for (int j = 0; j < n; j++) {
            if (i == 0 && j == 0) cur[j] = 1;
            else {
                int up = i > 0 ? prev[j] : 0;
                int left = j > 0 ? cur[j - 1] : 0;
                cur[j] = up + left;
            }
        }
        prev = cur;
    }

    return prev[n - 1];
}
```

⏱️ **Time Complexity:** O(m × n)  
📦 **Space Complexity:** O(n)

---

## ✅ Summary of Approaches

|Approach|Time Complexity|Space Complexity|Notes|
|---|---|---|---|
|Recursion|Exponential|O(m + n) call stack|TLE|
|Memoization (Top-down)|O(m × n)|O(m × n) + recursion stack|✅ Efficient|
|Tabulation (Bottom-up)|O(m × n)|O(m × n)|✅ Clean and fast|
|Space Optimization|O(m × n)|O(n)|✅ Best space|

---

## 🚀 Extension Ideas

- **Obstacle Grid:** Add check for obstacles in base case and transitions.
    
- **Minimum Path Sum:** Instead of counting paths, compute minimum cost to reach `(0, 0)`.
    
- **Print All Paths:** Modify recursion to carry a path list.
    
- **Path with Directions:** Store direction movement (`U`, `L`) in path strings.
    

---

Let me know if you want the **obstacle grid**, **path printing**, or **combinatorics formula** version too!