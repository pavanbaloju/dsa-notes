Here’s the full explanation, breakdown, and code for solving **“Number of Distinct Islands”** — a classic DFS + hashing + shape encoding problem.

---

## ✅ Problem: Leetcode 694 — Number of Distinct Islands

**Input:**

A binary matrix (`grid[][]`) containing only 0 and 1.  
1 represents land, 0 represents water.  
An island is a group of connected 1's (4-directionally: up, down, left, right).

**Task:**

Return the number of **distinct** islands.

Two islands are **distinct** if their **shapes** are different. Position does **not** matter.

---

## 💡 Key Idea

- You’re not just counting islands — you want to count **unique island shapes**.
    
- This means two islands that look the same (same structure) but in different locations should count as one.
    

---

## 🧠 Approach

### ✅ 1. DFS Traversal

Traverse each island (group of 1s) using DFS.

### ✅ 2. Normalize Shape

As you traverse, record the **relative movement** (e.g., "Right", "Down", etc.) from the **starting point**.

Example of shape encoding: `"O R D L U"`  
This helps ignore absolute positions.

### ✅ 3. Use HashSet

Store these **path strings** in a `Set`. The size of the set gives the number of distinct shapes.

---

## ✅ DFS-Based Java Code with Comments

```java
class Solution {
    public int numDistinctIslands(int[][] grid) {
        int rows = grid.length;
        int cols = grid[0].length;
        Set<String> shapes = new HashSet<>();

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (grid[i][j] == 1) {
                    StringBuilder path = new StringBuilder();
                    dfs(grid, i, j, path, "O"); // "O" = origin
                    shapes.add(path.toString());
                }
            }
        }

        return shapes.size();
    }

    private void dfs(int[][] grid, int i, int j, StringBuilder path, String dir) {
        int rows = grid.length;
        int cols = grid[0].length;

        if (i < 0 || j < 0 || i >= rows || j >= cols || grid[i][j] == 0)
            return;

        grid[i][j] = 0; // mark as visited
        path.append(dir); // record the move

        dfs(grid, i + 1, j, path, "D"); // Down
        dfs(grid, i - 1, j, path, "U"); // Up
        dfs(grid, i, j + 1, path, "R"); // Right
        dfs(grid, i, j - 1, path, "L"); // Left

        path.append("B"); // "B" = backtrack to avoid shape collision like L->R cancels each other
    }
}
```

---

## 🧪 Example

### Input:

```java
grid = [
  [1,1,0,0,0],
  [1,0,0,0,0],
  [0,0,0,1,1],
  [0,0,0,1,1]
]
```

### Output:

```
1
```

Explanation:

- There are 2 islands, both shaped like an “L”.
    
- Their DFS shape encoding is the same → only 1 distinct island.
    

---

## 🔍 Dry Run Example

For top-left island:

- Path: `O D R B B`
    

For bottom-right island:

- Path: `O D R B B`
    

Same shape → only 1 added to the set.

---

## 📊 Time & Space Complexity

|Metric|Complexity|
|---|---|
|Time|O(m × n)|
|Space (Recursion)|O(m × n)|
|Space (Set)|O(k × l)|

- where `k` is number of islands, and `l` is max shape size
    

---

## 🧠 Key Takeaways

|Concept|Details|
|---|---|
|Goal|Count **unique** island **shapes**|
|Graph Traversal|DFS / BFS on 2D grid|
|Uniqueness Mechanism|Encode shape using relative direction moves|
|Trick|Use backtrack ('B') to distinguish same-length paths|

---

Let me know if you want the **BFS version**, or to go deeper into **shape canonicalization (rotation/reflection)** for follow-ups.