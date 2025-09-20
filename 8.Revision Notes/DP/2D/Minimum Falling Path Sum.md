Here are **full structured notes** on **Minimum / Maximum Falling Path Sum in a Matrix**, from brute-force recursion to space-optimized DP.

---

## 🟩 Problem: Falling Path Sum (Min / Max)

Given an `n x n` matrix, a falling path starts at any element in the first row and chooses one element from the next row that is **either directly below**, **diagonally left**, or **diagonally right**. Return the **minimum (or maximum)** sum of a falling path from top to bottom.

---

### 🔸 Input Example

```text
matrix = [
  [2, 1, 3],
  [6, 5, 4],
  [7, 8, 9]
]
```

### 🔸 Output (Minimum Falling Path Sum): `13`

`1 → 4 → 8`

---

## ✅ Step-by-Step Approaches

---

### 🔸 1. **Brute Force Recursion**

#### ▶️ Idea:

Try all 3 possible directions from a cell `(i, j)`:

- Straight down → `(i+1, j)`
    
- Left diagonal → `(i+1, j-1)`
    
- Right diagonal → `(i+1, j+1)`
    

```java
int minPath(int i, int j, int[][] matrix) {
    int n = matrix.length;

    if (j < 0 || j >= n) return (int)1e9; // out of bounds
    if (i == 0) return matrix[0][j];      // base case: first row

    int up = matrix[i][j] + minPath(i - 1, j, matrix);
    int leftDiag = matrix[i][j] + minPath(i - 1, j - 1, matrix);
    int rightDiag = matrix[i][j] + minPath(i - 1, j + 1, matrix);

    return Math.min(up, Math.min(leftDiag, rightDiag));
}
```

To get the final answer:

```java
int result = Integer.MAX_VALUE;
for (int j = 0; j < n; j++) {
    result = Math.min(result, minPath(n - 1, j, matrix));
}
```

#### ⏱ Time: `O(3^n)`

#### 💾 Space: `O(n)` (stack depth)

---

### 🔸 2. **Memoization (Top-Down DP)**

#### ▶️ Idea:

Store results in `dp[i][j]` to avoid recalculating.

```java
int minPath(int i, int j, int[][] matrix, int[][] dp) {
    int n = matrix.length;

    if (j < 0 || j >= n) return (int)1e9;
    if (i == 0) return matrix[0][j];
    if (dp[i][j] != -1) return dp[i][j];

    int up = matrix[i][j] + minPath(i - 1, j, matrix, dp);
    int left = matrix[i][j] + minPath(i - 1, j - 1, matrix, dp);
    int right = matrix[i][j] + minPath(i - 1, j + 1, matrix, dp);

    return dp[i][j] = Math.min(up, Math.min(left, right));
}
```

Final result:

```java
int minFallingPathSum(int[][] matrix) {
    int n = matrix.length;
    int[][] dp = new int[n][n];
    for (int[] row : dp) Arrays.fill(row, -1);

    int min = Integer.MAX_VALUE;
    for (int j = 0; j < n; j++) {
        min = Math.min(min, minPath(n - 1, j, matrix, dp));
    }
    return min;
}
```

#### ⏱ Time: `O(n^2)`

#### 💾 Space: `O(n^2)` + stack

---

### 🔸 3. **Tabulation (Bottom-Up DP)**

#### ▶️ Idea:

Start from top row and compute the minimum falling path sum row by row.

```java
int minFallingPathSum(int[][] matrix) {
    int n = matrix.length;
    int[][] dp = new int[n][n];

    // Base case: copy the first row
    for (int j = 0; j < n; j++) {
        dp[0][j] = matrix[0][j];
    }

    for (int i = 1; i < n; i++) {
        for (int j = 0; j < n; j++) {
            int up = dp[i - 1][j];
            int left = (j > 0) ? dp[i - 1][j - 1] : (int)1e9;
            int right = (j < n - 1) ? dp[i - 1][j + 1] : (int)1e9;
            dp[i][j] = matrix[i][j] + Math.min(up, Math.min(left, right));
        }
    }

    int min = Integer.MAX_VALUE;
    for (int j = 0; j < n; j++) {
        min = Math.min(min, dp[n - 1][j]);
    }
    return min;
}
```

#### ⏱ Time: `O(n^2)`

#### 💾 Space: `O(n^2)`

---

### 🔸 4. **Space Optimized DP**

#### ▶️ Idea:

Use two 1D arrays `prev` and `curr` because we only need previous row at a time.

```java
int minFallingPathSum(int[][] matrix) {
    int n = matrix.length;
    int[] prev = new int[n];

    for (int j = 0; j < n; j++) {
        prev[j] = matrix[0][j];
    }

    for (int i = 1; i < n; i++) {
        int[] curr = new int[n];
        for (int j = 0; j < n; j++) {
            int up = prev[j];
            int left = (j > 0) ? prev[j - 1] : (int)1e9;
            int right = (j < n - 1) ? prev[j + 1] : (int)1e9;
            curr[j] = matrix[i][j] + Math.min(up, Math.min(left, right));
        }
        prev = curr;
    }

    int min = Integer.MAX_VALUE;
    for (int val : prev) {
        min = Math.min(min, val);
    }
    return min;
}
```

#### ⏱ Time: `O(n^2)`

#### 💾 Space: `O(n)`

---

## 🧠 Maximum Falling Path Sum Variant

To get **maximum** path instead of minimum:

- Just change all `Math.min()` to `Math.max()`
    
- Base cases remain the same
    

---

## ✅ Summary Table

|Approach|Time|Space|Notes|
|---|---|---|---|
|Recursion|`O(3^n)`|`O(n)`|Exponential, not usable|
|Memoization|`O(n^2)`|`O(n^2)`|Top-down with cache|
|Tabulation|`O(n^2)`|`O(n^2)`|Bottom-up DP|
|Space Optimized|`O(n^2)`|`O(n)`|Most efficient version|

---

Let me know if you'd like:

- Path reconstruction version
    
- Explanation on when to prefer triangular grid vs full matrix
    
- Visual dry-run on examples