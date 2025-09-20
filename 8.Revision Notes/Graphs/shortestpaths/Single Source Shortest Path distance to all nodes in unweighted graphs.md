Here's a complete guide to **Single Source Shortest Path (SSSP)** for **unweighted graphs**, where we compute the **shortest distance from a source node to all other nodes**:

---

## ✅ Problem Statement

Given an **unweighted graph** (edges all have the same cost, typically `1`), and a **source node**, compute the **shortest path distance** from the source to **every other node**.

- The shortest path is the **minimum number of edges** needed to reach each node.
    
- Graph may be:
    
    - **Undirected** or **Directed**
        
    - **Connected** or **Disconnected**
        

---

## ✅ Algorithm: **Breadth-First Search (BFS)**

### 🧠 Why BFS?

- BFS explores nodes in **layers** (i.e., nodes 1 edge away, 2 edges away, etc.).
    
- Since all edges have **equal weight** (1), BFS guarantees the **shortest path** in terms of number of edges.
    

---

## ✅ Input Format

- `n`: number of nodes (labeled `0` to `n-1`)
    
- `adj`: adjacency list `List<List<Integer>>`
    
- `src`: source node (starting point)
    

---

## ✅ Java Code

```java
public int[] shortestPathUnweightedGraph(int n, List<List<Integer>> adj, int src) {
    int[] dist = new int[n];
    Arrays.fill(dist, -1);  // Use -1 to represent unreachable nodes
    Queue<Integer> queue = new LinkedList<>();

    dist[src] = 0;
    queue.offer(src);

    while (!queue.isEmpty()) {
        int node = queue.poll();
        for (int neighbor : adj.get(node)) {
            if (dist[neighbor] == -1) {
                dist[neighbor] = dist[node] + 1;
                queue.offer(neighbor);
            }
        }
    }

    return dist;
}
```

---

## ✅ Example

### Graph:

```
0 -- 1
|    |
4    2
 \  /
   3
```

### Input:

```java
n = 5
adj = [
  [1, 4],    // 0
  [0, 2],    // 1
  [1, 3],    // 2
  [2, 4],    // 3
  [0, 3]     // 4
]
src = 0
```

### Output:

```
dist = [0, 1, 2, 2, 1]
```

---

## ✅ Time and Space Complexity

|Aspect|Complexity|
|---|---|
|Time|O(V + E)|
|Space|O(V) for dist + queue|

---

## ✅ Use Cases

- Maze-solving problems (grids as graphs)
    
- Unweighted road networks
    
- Minimum steps to reach a target (e.g., word ladder, puzzle states)
    
- Finding levels in a tree/graph
    

---

## 🧠 Common Variants

- **Print path** instead of just distance → store a `parent[]` array during BFS.
    
- **Multiple sources** → start BFS with all sources enqueued.
    
- **Grids (2D matrix)** → neighbors = 4 or 8 directions; treat each cell as a node.
    

---

## 🧪 Test Edge Cases

|Case|Expected Behavior|
|---|---|
|Disconnected node|Distance remains `-1`|
|Graph with cycles|Still works (BFS won't revisit visited nodes)|
|Source = target|Distance is `0`|
|Tree (acyclic)|BFS still works|

---
Great question. The **BFS-based shortest path algorithm** for **unweighted graphs** works **only under specific assumptions**. Let's clarify **when and why it fails**:

---

## ❌ When This Algorithm **Fails**

### 1. **Weighted Graphs (Even Uniform Weights ≠ 1)**

**Why it fails:**  
BFS assumes **unit cost (1)** for each edge. If the graph has:

- Weights like 2, 5, or 0.5
    
- Even if all edges have equal but non-1 weights (e.g., weight 10)
    

Then **BFS does not find the correct minimum total weight**, only the minimum **number of edges**.

**Example:**

```text
Graph:
0 --(10)--> 1
 \        /
  \(1)  (1)
     > 2
```

- BFS from node 0 would reach 1 via 0→1 (edge weight 10).
    
- But the optimal path is 0→2→1 with total weight 2.
    
- BFS would not explore that because it doesn't account for edge weights.
    

✅ **Correct Algorithm:** Use **Dijkstra’s Algorithm** for weighted graphs.

---

### 2. **Negative Edge Weights**

**Why it fails:**  
BFS doesn’t account for **negative weights**. But even Dijkstra fails in this case.

✅ **Correct Algorithm:** Use **Bellman-Ford Algorithm** for graphs with negative weights.

---

### 3. **Graph Is Not Properly Represented**

- If adjacency list is incorrect (e.g., directed edges treated as undirected)
    
- If isolated/disconnected nodes are not in the list
    

**Effect:** Some nodes will be **skipped** or **visited incorrectly**, leading to invalid distances.

---

### 4. **Grids with Special Constraints**

In grid-based problems (like shortest path in a matrix):

- If certain directions are blocked
    
- Or movement has **different costs per direction**
    

Then plain BFS may be insufficient.

✅ Use BFS with condition checks or **0-1 BFS** / **Dijkstra** if weights are involved.

---

### 5. **Multiple Weights on Same Edge**

Some problems allow:

- Multiple paths between same nodes with **different weights**
    

BFS can’t distinguish between them because it just sees an edge exists.

✅ Use a priority queue-based approach (Dijkstra).

---

## ✅ Summary Table

|Graph Type|BFS Works?|Correct Algorithm|
|---|---|---|
|Unweighted|✅ Yes|BFS|
|Weighted (all weights = 1)|✅ Yes|BFS|
|Weighted (non-1 weights)|❌ No|Dijkstra|
|Weighted (negative weights)|❌ No|Bellman-Ford|
|Grid with uniform steps|✅ Yes|BFS|
|Grid with varying step cost|❌ No|Dijkstra or 0-1 BFS|
|Multiple sources|✅ Yes|Multi-source BFS|

---

Let me know if you want:

- Dijkstra’s full notes
    
- Bellman-Ford algorithm explanation
    
- BFS with path reconstruction
    
- 0-1 BFS (for weights 0 and 1)