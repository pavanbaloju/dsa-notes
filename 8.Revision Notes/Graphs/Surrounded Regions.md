Here's the complete guide to solving **Surrounded Regions** (Leetcode 130) — with concept, strategy, dry run, and code.

---

## 🧠 Problem Intuition

Given an `m x n` board containing `'X'` and `'O'`, capture all regions surrounded by `'X'`.

A region is **captured** if it is **completely surrounded by 'X'** (i.e., not connected to a border `'O'`).  
Captured `'O'`s should be flipped to `'X'`.

---

## ✅ Problem Summary

**Input:**

```txt
board = [
  ['X','X','X','X'],
  ['X','O','O','X'],
  ['X','X','O','X'],
  ['X','O','X','X']
]
```

**Output:**

```txt
[
  ['X','X','X','X'],
  ['X','X','X','X'],
  ['X','X','X','X'],
  ['X','O','X','X']
]
```

Explanation:

- `'O'`s connected to **border** remain `'O'`.
    
- Internal `'O'`s not connected to border are captured.
    

---

## 🚀 Strategy: Mark Border-Connected `'O'`s

1. **Traverse all border cells**.
    
2. For each border `'O'`, do **DFS or BFS** to mark all connected `'O'`s (safe ones).
    
3. After traversal:
    
    - Flip unmarked `'O'` → `'X'` (captured).
        
    - Revert marked `'T'` → `'O'`.
        

---

## ✅ Steps Breakdown

- Step 1: Loop over border rows and columns
    
- Step 2: If `'O'`, mark with temporary symbol (e.g., `'T'`)
    
- Step 3: Traverse from `'T'` using DFS/BFS
    
- Step 4: Final pass: Flip all `'O'` → `'X'`, `'T'` → `'O'`
    

---

## ✅ Java Code (DFS)

```java
class Solution {
    public void solve(char[][] board) {
        int m = board.length;
        int n = board[0].length;

        // Step 1: Mark border-connected 'O's with 'T'
        for (int i = 0; i < m; i++) {
            if (board[i][0] == 'O') dfs(board, i, 0);
            if (board[i][n - 1] == 'O') dfs(board, i, n - 1);
        }
        for (int j = 0; j < n; j++) {
            if (board[0][j] == 'O') dfs(board, 0, j);
            if (board[m - 1][j] == 'O') dfs(board, m - 1, j);
        }

        // Step 2: Flip captured 'O' to 'X', and 'T' back to 'O'
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == 'O') board[i][j] = 'X';
                if (board[i][j] == 'T') board[i][j] = 'O';
            }
        }
    }

    private void dfs(char[][] board, int i, int j) {
        int m = board.length;
        int n = board[0].length;

        if (i < 0 || j < 0 || i >= m || j >= n || board[i][j] != 'O') return;

        board[i][j] = 'T'; // Temporary marker

        dfs(board, i + 1, j);
        dfs(board, i - 1, j);
        dfs(board, i, j + 1);
        dfs(board, i, j - 1);
    }
}
```

---

## 🧠 Dry Run on Input

```txt
[
  ['X','X','X','X'],
  ['X','O','O','X'],
  ['X','X','O','X'],
  ['X','O','X','X']
]
```

- Only (3,1) is a border `'O'` → mark (3,1) as `'T'`
    
- No other border `'O'`
    

Final board after DFS:

```txt
[
  ['X','X','X','X'],
  ['X','O','O','X'],
  ['X','X','O','X'],
  ['X','T','X','X']
]
```

- Flip unmarked `'O'` → `'X'`
    
- Revert `'T'` → `'O'`
    

---

## 📊 Time & Space Complexity

|Metric|Value|
|---|---|
|Time|O(m × n)|
|Space (DFS)|O(m × n) recursion|
|Space (BFS)|O(m × n) queue|

---

## ✅ Summary

|Concept|Notes|
|---|---|
|Type|Matrix + Graph traversal|
|Technique|DFS/BFS from border|
|Capture condition|`'O'`s **not** connected to border|
|Temporary marker|`'T'` to distinguish safe `'O'`s|

---

Let me know if you want:

- **BFS version**
    
- **Union-Find version** (less common)
    
- **Dry run diagram for interview prep**