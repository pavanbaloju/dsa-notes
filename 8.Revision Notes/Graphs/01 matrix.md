The **0/1 Matrix problem** is a classic BFS-based flood-fill style problem, typically seen as:

---

## 🔷 Problem: Leetcode 542 — **01 Matrix**

### 📌 Statement:

Given an `m x n` binary matrix `mat` containing only `0` and `1`, return a matrix `dist` of the same size such that:

> Each cell `dist[i][j]` contains the **distance to the nearest `0`** in the original matrix.

---

## ✅ Example:

**Input:**

```
mat = [
 [0,0,0],
 [0,1,0],
 [1,1,1]
]
```

**Output:**

```
[
 [0,0,0],
 [0,1,0],
 [1,2,1]
]
```

---

## ✅ Intuition

This is a **multi-source shortest path** problem where all the `0`s act as **sources**, and we are asked to compute the minimum distance from each `1` to the nearest `0`.

---

## ✅ Approach: **Multi-source BFS**

1. Push all the `0`s into the queue initially.
    
2. For every cell in the queue, perform BFS and update its 4 neighbors if:
    
    - the neighbor has value `1`, and
        
    - hasn't been updated (i.e., has `dist == -1`)
        
3. The first time we reach a `1`, it’s guaranteed to be the **shortest distance** from any `0`.
    

---

## ✅ Java Code (BFS)

```java
class Solution {
    public int[][] updateMatrix(int[][] mat) {
        int m = mat.length, n = mat[0].length;
        int[][] dist = new int[m][n];
        boolean[][] visited = new boolean[m][n];
        Queue<int[]> q = new LinkedList<>();

        // Step 1: Push all 0s to queue, mark visited
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (mat[i][j] == 0) {
                    q.offer(new int[]{i, j});
                    visited[i][j] = true;
                }
            }
        }

        // Directions: up, down, left, right
        int[][] dirs = {{-1,0}, {1,0}, {0,-1}, {0,1}};

        // Step 2: BFS from all 0s
        while (!q.isEmpty()) {
            int[] cell = q.poll();
            int i = cell[0], j = cell[1];

            for (int[] dir : dirs) {
                int ni = i + dir[0], nj = j + dir[1];

                if (ni >= 0 && nj >= 0 && ni < m && nj < n && !visited[ni][nj]) {
                    dist[ni][nj] = dist[i][j] + 1;
                    visited[ni][nj] = true;
                    q.offer(new int[]{ni, nj});
                }
            }
        }

        return dist;
    }
}
```

---

## ✅ Time & Space Complexity

|Metric|Complexity|
|---|---|
|Time|O(m × n)|
|Space|O(m × n)|

---

## 🔁 Related Problems

|Problem|Notes|
|---|---|
|Leetcode 994 — Rotting Oranges|Similar BFS flood fill with time tracking|
|Leetcode 286 — Walls and Gates|Very similar — shortest distance to gate|
|Leetcode 1091 — Shortest Path in Binary Matrix|Path from (0,0) to (n-1,n-1)|
|Leetcode 200 — Number of Islands|Classic DFS/BFS count regions|

---

Would you like:

- DFS version (less efficient)?
    
- A dry run on a matrix?
    
- Java version with no `visited` array (reuse `mat`)?
    

Let me know how you want to study it.