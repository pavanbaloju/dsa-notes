Here are **full notes** on the **Max Area of Island** problem using **DFS** and **BFS** in Java, including explanation, time/space complexities, and commented code.

---

## 🧠 Problem Summary

**Leetcode 695: Max Area of Island**  
Given a binary 2D grid, where `1` represents land and `0` represents water, return the **area of the largest island** (connected group of `1`s). An island is **connected 4-directionally** (up, down, left, right).

---

## 🧾 Input / Output

- **Input**: 2D int array `grid` of size `m x n`
    
- **Output**: Integer (maximum area of any island)
    

---

## ✅ Constraints

- Grid size: up to 50 x 50
    
- Only `0` and `1` in the grid
    
- Multiple islands may exist
    

---

## 🔍 Approach 1: DFS (Recursive)

### 🧩 Idea

- Traverse each cell in the grid.
    
- If the cell is land (`1`), run a DFS to calculate the area of the island.
    
- Mark visited land (`1`) as water (`0`) to avoid revisiting.
    
- Track the max area found during traversal.
    

---

### 📦 Time and Space Complexity

- **Time**: `O(m * n)` — each cell visited at most once
    
- **Space**: `O(m * n)` — recursion stack in the worst case
    

---

### ✅ DFS Java Code

```java
public class Solution {
    public int maxAreaOfIsland(int[][] grid) {
        int maxArea = 0;

        for (int row = 0; row < grid.length; row++) {
            for (int col = 0; col < grid[0].length; col++) {
                if (grid[row][col] == 1) {
                    int area = dfs(grid, row, col);
                    maxArea = Math.max(maxArea, area);
                }
            }
        }

        return maxArea;
    }

    private int dfs(int[][] grid, int row, int col) {
        // Out of bounds or water or already visited
        if (row < 0 || col < 0 || row >= grid.length || col >= grid[0].length || grid[row][col] != 1) {
            return 0;
        }

        // Mark visited
        grid[row][col] = 0;

        // Count current cell + explore all 4 directions
        int area = 1;
        area += dfs(grid, row + 1, col);
        area += dfs(grid, row - 1, col);
        area += dfs(grid, row, col + 1);
        area += dfs(grid, row, col - 1);

        return area;
    }
}
```

---

## 🔁 Approach 2: BFS (Queue)

### 🧩 Idea

- Instead of recursion, use a **queue** to do level-order traversal.
    
- For each land cell (`1`), run BFS and count the area.
    

---

### 📦 Time and Space Complexity

- **Time**: `O(m * n)`
    
- **Space**: `O(m * n)` for queue in worst case
    

---

### ✅ BFS Java Code

```java
import java.util.*;

public class Solution {
    public int maxAreaOfIsland(int[][] grid) {
        int maxArea = 0;
        int m = grid.length, n = grid[0].length;

        for (int row = 0; row < m; row++) {
            for (int col = 0; col < n; col++) {
                if (grid[row][col] == 1) {
                    int area = bfs(grid, row, col);
                    maxArea = Math.max(maxArea, area);
                }
            }
        }

        return maxArea;
    }

    private int bfs(int[][] grid, int row, int col) {
        int area = 0;
        Queue<int[]> queue = new LinkedList<>();
        queue.offer(new int[]{row, col});
        grid[row][col] = 0; // mark visited

        int[][] directions = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};

        while (!queue.isEmpty()) {
            int[] curr = queue.poll();
            area++;

            for (int[] dir : directions) {
                int r = curr[0] + dir[0];
                int c = curr[1] + dir[1];

                if (r >= 0 && r < grid.length && c >= 0 && c < grid[0].length && grid[r][c] == 1) {
                    queue.offer(new int[]{r, c});
                    grid[r][c] = 0; // mark visited
                }
            }
        }

        return area;
    }
}
```

---

## 💡 Intuition

- Treat each `1` as a potential starting point of a new island.
    
- From there, explore all connected `1`s.
    
- We don't need a separate `visited[][]` because we mutate the original grid (setting `1 -> 0` after visiting).
    

---

## 🔁 Follow-ups

1. Can you return coordinates of the largest island?
    
2. Modify to work with **diagonal connections**.
    
3. Instead of 2D grid, do the same for a graph.
    

---

Let me know if you'd like the **dry run** of the algorithm, or if you want to extend this to count number of islands, return all island sizes, or solve in-place without modifying input.