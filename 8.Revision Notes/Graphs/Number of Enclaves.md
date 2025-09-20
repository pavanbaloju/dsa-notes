Here’s the complete **“Number of Enclaves”** problem explanation using a **flood fill (multisource BFS/DFS)** approach:

---

## ✅ Problem: Leetcode 1020 — Number of Enclaves

### 📌 Statement:

You are given a binary matrix `grid[][]` of size `m x n`.

- `0` represents water
    
- `1` represents land
    

A **land cell** can move **up, down, left, right** to other land cells.

> A land cell is an **enclave** if it **cannot** walk off the boundary of the grid in any number of moves.

### 👉 Your task:

Return the **number of enclave land cells**.

---

## ✅ Intuition

Any land cell (`1`) that is **connected to the boundary** is **not** an enclave.

So, if we **flood fill** from all the boundary land cells (multisource BFS/DFS), and mark all reachable land cells as visited, the remaining land cells are **enclaves**.

---

## 🧠 Approach: Flood Fill from Borders (Multisource BFS/DFS)

### Steps:

1. **Flood fill** all land (`1`) cells that are **connected to borders**.
    
    - These cannot be enclaves.
        
2. After marking all border-connected land, **count the remaining `1`s** in the grid.
    
    - These are **trapped** — true enclaves.
        

---

## ✅ DFS Code (Java) with Comments

```java
class Solution {
    public int numEnclaves(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;

        // Step 1: Flood fill from boundary land cells
        for (int i = 0; i < m; i++) {
            dfs(grid, i, 0);         // left border
            dfs(grid, i, n - 1);     // right border
        }
        for (int j = 0; j < n; j++) {
            dfs(grid, 0, j);         // top border
            dfs(grid, m - 1, j);     // bottom border
        }

        // Step 2: Count remaining land cells (1s) — these are enclaves
        int count = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1) count++;
            }
        }

        return count;
    }

    private void dfs(int[][] grid, int i, int j) {
        int m = grid.length, n = grid[0].length;

        if (i < 0 || j < 0 || i >= m || j >= n || grid[i][j] == 0) return;

        grid[i][j] = 0; // Mark as visited (water)

        // Visit all 4 directions
        dfs(grid, i + 1, j);
        dfs(grid, i - 1, j);
        dfs(grid, i, j + 1);
        dfs(grid, i, j - 1);
    }
}
```

---

## ✅ BFS Version (Multisource Flood Fill)

You can also do this with **BFS from all border land cells**:

```java
class Solution {
    public int numEnclaves(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        Queue<int[]> queue = new LinkedList<>();

        // Step 1: Add all border land cells to queue
        for (int i = 0; i < m; i++) {
            if (grid[i][0] == 1) queue.offer(new int[]{i, 0});
            if (grid[i][n - 1] == 1) queue.offer(new int[]{i, n - 1});
        }
        for (int j = 0; j < n; j++) {
            if (grid[0][j] == 1) queue.offer(new int[]{0, j});
            if (grid[m - 1][j] == 1) queue.offer(new int[]{m - 1, j});
        }

        // Step 2: Flood fill all reachable land from borders
        while (!queue.isEmpty()) {
            int[] cell = queue.poll();
            int i = cell[0], j = cell[1];

            if (i < 0 || j < 0 || i >= m || j >= n || grid[i][j] == 0) continue;

            grid[i][j] = 0; // Mark as visited

            queue.offer(new int[]{i + 1, j});
            queue.offer(new int[]{i - 1, j});
            queue.offer(new int[]{i, j + 1});
            queue.offer(new int[]{i, j - 1});
        }

        // Step 3: Count remaining land cells
        int count = 0;
        for (int i = 0; i < m; i++)
            for (int j = 0; j < n; j++)
                if (grid[i][j] == 1) count++;

        return count;
    }
}
```

---

## 🔍 Dry Run

```text
Initial:
[0,0,0,0]
[1,0,1,0]
[0,1,1,0]
[0,0,0,0]

Only 1 island (1s) in center is not connected to any border => Enclave size = 3
```

---

## 📊 Time & Space Complexity

|Metric|Complexity|
|---|---|
|Time|O(m × n)|
|Space (DFS)|O(m × n) recursion stack|
|Space (BFS)|O(m × n) queue|

---

## ✅ Summary

|Step|Purpose|
|---|---|
|Flood fill from borders|Eliminate all land connected to border|
|Count remaining `1`s|Get enclave cells only|
|DFS or BFS|Both work, pick based on preference|

---

Let me know if you’d like:

- Union-Find version (less common here)
    
- 2D Grid BFS/DFS cheatsheet
    
- A practice list of similar problems (e.g. Surrounded Regions, Number of Islands, etc.)