Here's a **complete guide with full notes** on the **Rotting Oranges** problem (Leetcode #994), including intuition, approach, edge cases, code with comments, and time/space complexity.

---

### 🔷 Problem Statement

You are given an `m x n` grid where:

- `0` = empty cell
    
- `1` = fresh orange
    
- `2` = rotten orange
    

Every minute, a rotten orange can rot its adjacent fresh oranges (up/down/left/right).

**Return the minimum number of minutes** that must elapse until **no fresh orange remains**.  
If impossible, return `-1`.

---

### 🔶 Intuition

- All initially rotten oranges rot adjacent fresh ones in 1 minute.
    
- We need to simulate this minute-by-minute "spread".
    
- This is a classic **multi-source BFS**:
    
    - All rotten oranges are starting points (sources).
        
    - We expand layer by layer to rot fresh oranges.
        

---

### 🔷 Approach: Multi-Source BFS

1. **Push all initial rotten oranges** into a queue with their position and time (minute = 0).
    
2. **Count total fresh oranges**.
    
3. Start BFS:
    
    - For each rotten orange, spread to its 4 neighbors.
        
    - If a neighbor is fresh, rot it and push to queue with time + 1.
        
    - Reduce the fresh orange count.
        
4. If at the end, fresh count is `0`, return time. Else return `-1`.
    

---

### 🔶 Java Code with Comments

```java
import java.util.*;

public class RottingOranges {

    static class Pair {
        int row, col, time;
        Pair(int r, int c, int t) {
            this.row = r;
            this.col = c;
            this.time = t;
        }
    }

    public int orangesRotting(int[][] grid) {
        int rows = grid.length;
        int cols = grid[0].length;

        Queue<Pair> queue = new LinkedList<>();
        int freshCount = 0;

        // Step 1: Count fresh oranges and add rotten oranges to queue
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (grid[i][j] == 2) {
                    queue.offer(new Pair(i, j, 0));
                } else if (grid[i][j] == 1) {
                    freshCount++;
                }
            }
        }

        int time = 0;
        int[][] directions = {{-1,0}, {1,0}, {0,-1}, {0,1}}; // up, down, left, right

        // Step 2: BFS to rot oranges
        while (!queue.isEmpty()) {
	            Pair current = queue.poll();
            int r = current.row;
            int c = current.col;
            time = current.time; // keep updating time as we go deeper in BFS

            for (int[] dir : directions) {
                int nr = r + dir[0];
                int nc = c + dir[1];

                // if within bounds and fresh
                if (nr >= 0 && nr < rows && nc >= 0 && nc < cols && grid[nr][nc] == 1) {
                    grid[nr][nc] = 2; // rot it
                    freshCount--;     // reduce count
                    queue.offer(new Pair(nr, nc, time + 1));
                }
            }
        }

        // Step 3: If fresh oranges remain, return -1
        return freshCount == 0 ? time : -1;
    }
}
```

---

### 🔷 Time and Space Complexity

#### ✅ Time Complexity: **O(m * n)**

- Each cell is processed at most once.
    
- BFS loop runs for each orange.
    

#### ✅ Space Complexity: **O(m * n)**

- Queue stores positions of rotten oranges.
    
- In worst case, all oranges are rotten/fresh.
    

---

### 🔶 Edge Cases

|Grid|Output|Reason|
|---|---|---|
|`[[0]]`|`0`|No oranges at all|
|`[[1]]`|`-1`|Cannot rot the only fresh orange|
|`[[2]]`|`0`|Already rotten|
|`[[2,1,1],[1,1,0],[0,1,1]]`|`4`|Classic BFS spread|

---

### 🔷 BFS vs DFS?

- DFS won't work here because time spreads simultaneously — i.e., all adjacent fresh oranges rot **in parallel**, not in sequence.
    
- BFS is ideal to simulate **minimum steps / minutes**.
    

---

### 🔶 Tips

- Treat BFS as a "flood" of rot across the matrix.
    
- Use multi-source BFS for any problem where **multiple starting points expand simultaneously**.
    
- Always update time at the moment of popping from the queue, not when pushing.
    

---

Let me know if you want a **visual dry run**, or want this adapted to C++ or Python.