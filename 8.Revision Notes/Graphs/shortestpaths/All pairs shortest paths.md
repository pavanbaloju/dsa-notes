Here are **complete notes** on the **All Pairs Shortest Path (APSP)** problem, focusing on the **Floyd-Warshall algorithm**, which is the most common algorithm used for this.

---

## 🔍 Problem: All Pairs Shortest Path

> Given a graph with `n` vertices (0-indexed from `0` to `n - 1`) and weighted edges (can be negative, but **no negative cycles**), compute the shortest distances between every pair of vertices.

---

## ✅ When to Use Floyd-Warshall?

- You want **shortest paths between all pairs** of nodes.
    
- Graph size is **small** (e.g., `n ≤ 500`), since time complexity is `O(n³)`.
    
- Graph **may have negative weights**, but **no negative cycles**.
    

---

## 📚 Time and Space Complexity

|Metric|Value|
|---|---|
|Time Complexity|O(V³)|
|Space Complexity|O(V²)|

---

## 🧠 Intuition

- Use **dynamic programming**.
    
- Maintain a matrix `dist[i][j]` where each cell represents the shortest path from node `i` to `j`.
    
- For each intermediate node `k`, check if going from `i → k → j` is **shorter** than `i → j`.
    
- Update the matrix accordingly.
    

---

## 🧾 Input

- `n`: number of vertices
    
- `edges[][]`: each edge is `[u, v, weight]`
    

---

## 🧩 Output

- A `dist[i][j]` matrix of shortest distances from node `i` to `j`
    

---

## ✅ Algorithm Steps

1. **Initialize matrix**:
    
    - `dist[i][i] = 0`
        
    - If edge from `i → j`, then `dist[i][j] = weight`
        
    - Else `dist[i][j] = ∞`
        
2. **Iterate over all pairs for each intermediate node `k`**:
    
    - If `dist[i][k] + dist[k][j] < dist[i][j]`, then update.
        
3. **Check for negative cycles**: If `dist[i][i] < 0` for any `i`, there is a cycle.
    

---

## ✅ Java Code: Floyd-Warshall

```java
public class FloydWarshall {

    static final int INF = 1000000000; // Large number to represent ∞

    public static int[][] floydWarshall(int n, int[][] edges) {
        int[][] dist = new int[n][n];

        // Step 1: Initialize distances
        for (int i = 0; i < n; i++) {
            Arrays.fill(dist[i], INF);
            dist[i][i] = 0;
        }

        for (int[] edge : edges) {
            int u = edge[0], v = edge[1], w = edge[2];
            dist[u][v] = w;
        }

        // Step 2: Dynamic Programming
        for (int k = 0; k < n; k++) {
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    if (dist[i][k] < INF && dist[k][j] < INF) {
                        dist[i][j] = Math.min(dist[i][j], dist[i][k] + dist[k][j]);
                    }
                }
            }
        }

        // Step 3: Negative Cycle Check
        for (int i = 0; i < n; i++) {
            if (dist[i][i] < 0) {
                throw new RuntimeException("Negative weight cycle detected");
            }
        }

        return dist;
    }

    // Sample usage
    public static void main(String[] args) {
        int n = 4;
        int[][] edges = {
            {0, 1, 5},
            {0, 3, 10},
            {1, 2, 3},
            {2, 3, 1}
        };

        int[][] result = floydWarshall(n, edges);

        for (int i = 0; i < n; i++) {
            System.out.println("From node " + i + ": " + Arrays.toString(result[i]));
        }
    }
}
```

---

## 🧪 Edge Cases

- **Disconnected nodes**: Remain `INF` in matrix.
    
- **Negative cycle**: Detected via `dist[i][i] < 0`.
    
- **Self-loops**: Handled with `dist[i][i] = 0` at initialization.
    

---

## 📦 Output Interpretation

After running the algorithm:

- `dist[i][j] = shortest path from node i to j`
    
- If `dist[i][j] == INF`, then `j` is not reachable from `i`
    

---

## 🧭 If you want the actual paths (not just distances)?

Use a `parent[i][j]` matrix and reconstruct paths by tracing predecessors.  
Let me know if you want this version too.

---

Great question. Let’s break down **how this line detects a negative weight cycle in Floyd-Warshall**:

---

## 🔍 Line in Question

```java
for (int i = 0; i < n; i++) {
    if (dist[i][i] < 0) {
        throw new RuntimeException("Negative weight cycle detected");
    }
}
```

---

## 💡 What does `dist[i][i]` mean?

In the Floyd-Warshall algorithm, `dist[i][i]` represents the **shortest path cost to go from node `i` back to itself** — i.e., the cost of the **shortest cycle that starts and ends at `i`**.

---

## 🚨 Why is `dist[i][i] < 0` a red flag?

- Normally, the shortest path from a node to itself should be `0` (no movement).
    
- If `dist[i][i] < 0`, it means there exists a path from `i → ... → i` where the total sum of edge weights is negative.
    
- In other words, **there’s a cycle starting and ending at `i` with total weight < 0**.
    
- This means a **negative weight cycle exists**.
    

---

## 🔄 How does Floyd-Warshall find this?

During its update step:

```java
if (dist[i][k] + dist[k][j] < dist[i][j])
    dist[i][j] = dist[i][k] + dist[k][j];
```

it considers **all possible paths** via intermediate nodes. So, if a negative cycle exists, the algorithm keeps improving the path that loops through it, and eventually `dist[i][i]` becomes negative.

---

## 🧠 Real Example

Suppose you have a graph:

```
0 → 1 (weight 1)
1 → 2 (weight -1)
2 → 0 (weight -1)
```

This forms a cycle: `0 → 1 → 2 → 0`

Total weight: `1 + (-1) + (-1) = -1`

So, Floyd-Warshall will eventually find that `dist[0][0] = -1`, and this line:

```java
if (dist[0][0] < 0)
```

will detect it and throw an error.

---

## ✅ Summary

- `dist[i][i] < 0` means there is a negative-weight cycle reachable from node `i`.
    
- Floyd-Warshall can **detect** but **not handle** negative weight cycles — you should **abort** or throw an exception if one is found.
    
- This check is essential to ensure that the algorithm's result is valid.
    

Let me know if you'd like to visualize this with a diagram or example trace of matrix updates.