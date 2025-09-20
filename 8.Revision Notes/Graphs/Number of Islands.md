Here are your **full notes for the "Number of Islands"** problem (LeetCode 200), including the problem breakdown, intuition, BFS and DFS solutions, complexity, common mistakes, and related problems.

---

## ✅ Number of Islands – Full Notes

**LeetCode 200: Number of Islands**  
This is a **graph traversal** problem applied on a 2D grid.

---

### 🔹 Problem Statement

You are given a 2D grid `grid` of `'1'`s (land) and `'0'`s (water). An **island** is a group of connected `'1'`s **connected 4-directionally** (up/down/left/right).  
Return the **number of islands**.

---

### 🔹 Input / Output

**Input:**

- A 2D `char[][] grid`
    
- Each cell is either `'1'` (land) or `'0'` (water)
    

**Output:**

- An integer: number of islands
    

---

### 🔹 Example

```text
Input:
11110
11010
11000
00000

Output: 1
```

```text
Input:
11000
11000
00100
00011

Output: 3
```

---

### 🔹 Core Idea

You are doing **multiple DFS/BFS traversals**:

- Traverse each cell in the grid.
    
- When you find a `'1'`, that’s the **start of a new island**.
    
- Do a BFS or DFS from there to **mark all connected `'1'`s as visited** (change to `'0'` or use visited matrix).
    
- Increment island count.
    

---

### ✅ DFS Solution (Mutating grid)

```java
public int numIslands(char[][] grid) {
    if (grid == null || grid.length == 0) return 0;

    int count = 0;
    int rows = grid.length, cols = grid[0].length;

    for (int r = 0; r < rows; r++) {
        for (int c = 0; c < cols; c++) {
            if (grid[r][c] == '1') {
                count++;
                dfs(grid, r, c);
            }
        }
    }

    return count;
}

private void dfs(char[][] grid, int r, int c) {
    if (r < 0 || r >= grid.length || c < 0 || c >= grid[0].length || grid[r][c] == '0') return;

    grid[r][c] = '0'; // Mark visited

    dfs(grid, r + 1, c);
    dfs(grid, r - 1, c);
    dfs(grid, r, c + 1);
    dfs(grid, r, c - 1);
}
```

---

### ✅ BFS Solution (Mutating grid)

```java
public int numIslands(char[][] grid) {
    if (grid == null || grid.length == 0) return 0;

    int rows = grid.length, cols = grid[0].length;
    int islands = 0;
    int[][] dirs = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};

    for (int r = 0; r < rows; r++) {
        for (int c = 0; c < cols; c++) {
            if (grid[r][c] == '1') {
                islands++;

				// bfs start
                Queue<int[]> queue = new LinkedList<>();
                queue.offer(new int[]{r, c});
                grid[r][c] = '0'; // ✅ Mark visited when enqueuing

                while (!queue.isEmpty()) {
                    int[] pos = queue.poll();
                    for (int[] dir : dirs) {
                        int nr = pos[0] + dir[0], nc = pos[1] + dir[1];
                        if (nr >= 0 && nr < rows && nc >= 0 && nc < cols && grid[nr][nc] == '1') {
                            queue.offer(new int[]{nr, nc});
                            grid[nr][nc] = '0'; // ✅ Mark as visited
                        }
                    }
                }
            }
        }
    }

    return islands;
}
```

---

### 🔹 Time and Space Complexity

|Approach|Time Complexity|Space Complexity|
|---|---|---|
|DFS|O(N × M)|O(N × M) recursion stack (worst case)|
|BFS|O(N × M)|O(N × M) queue in worst case|

> N = number of rows, M = number of cols  
> Every cell is visited **at most once**

---

### 🔹 Why mark `'1' → '0'` when visited?

- Prevents revisiting
    
- No need for extra `visited[][]` array (space efficient)
    
- Also ensures BFS/DFS stops after consuming one island
    

---

### 🔹 Common Mistakes

- ❌ Forgetting boundary checks in DFS/BFS
    
- ❌ Not marking visited correctly (in BFS, **mark when enqueueing**, not dequeueing)
    
- ❌ Missing one direction (only 3 out of 4)
    
- ❌ Modifying input grid when it’s not allowed – in interviews, clarify
    

---

### 🔹 Variants to Practice

|Problem|Variation|
|---|---|
|LeetCode 695 – Max Area of Island|Return area instead of count|
|LeetCode 130 – Surrounded Regions|Need to capture only safe regions|
|LeetCode 694 – Number of Distinct Islands|Compare island shapes|
|LeetCode 733 – Flood Fill|Recolor region instead of count|
|LeetCode 286 – Walls and Gates|BFS from multiple sources|
|LeetCode 1020 – Number of Enclaves|Land not touching boundary|

---

### 🔹 Interview Strategy

- Choose DFS if:
    
    - You want concise recursion
        
    - Stack depth is not too big
        
- Choose BFS if:
    
    - You want to avoid recursion stack overflow
        
    - You need to process in layers (multi-source BFS)
        

---

### 🔹 Sample Dry Run

```text
Grid:
1 1 0 0 0
1 1 0 0 0
0 0 1 0 0
0 0 0 1 1

- Start at (0,0): do DFS/BFS to mark entire top-left island
- Then (2,2): new island
- Then (3,3): new island
→ Total = 3 islands
```

---

### ✅ Summary Table

|Topic|Value|
|---|---|
|Problem Type|Matrix BFS/DFS|
|Graph Model|Implicit graph on 2D grid|
|Traversal|4-directional|
|Visited Mark|Mutate to `'0'`|
|Output|Count of traversals|

---

Let me know if you want to add **Union Find (DSU)** version or convert this to a **template-based grid traversal format**.