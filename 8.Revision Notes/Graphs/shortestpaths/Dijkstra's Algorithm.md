Finding the shortest path distances from a single source in a graph with non-negative weighted edges

---

## ✅ Dijkstra’s Algorithm – Full Notes

---

### 🧠 **Core Idea**

Dijkstra’s algorithm finds the shortest path from a **source node** to **all other nodes** in a graph with **non-negative edge weights**.

---

### 🧾 Input

- A weighted graph `G` with `n` nodes and `m` edges.
    
- Each edge has a **non-negative weight**.
    
- A source node `src`.
    

---

### 🎯 Output

- Shortest path **distances** from `src` to all other nodes.
    
- Optional: Actual **paths** (using a parent map).
    

---

### ✅ When to Use

- When graph edges have **non-negative weights**.
    
- To find **shortest distances from a single source** to all nodes.
    

---

### ❗ When Not to Use

- If the graph has **negative weights** → use **Bellman-Ford**.
    
- If you only care about reaching one destination and not all → consider A* or early-exit Dijkstra.
    

---

### 🧮 Time & Space Complexity

| Operation             | Using PriorityQueue (Binary Heap) |
| --------------------- | --------------------------------- |
| Time (Adj List)       | O((V + E) * log V)                |
| Space (Distance + PQ) | O(V + E)                          |

---

### 📚 Data Structures Used

- `PriorityQueue` (min-heap): always process the node with **smallest tentative distance**.
    
- `distance[]`: holds current shortest distances.
    
- `visited[]` or inside heap: avoid reprocessing outdated distances.
    
- `parent[]`: (optional) for path reconstruction.
    

---

### ✅ Java Implementation

```java
import java.util.*;

class Pair {
    int node, weight;
    Pair(int node, int weight) {
        this.node = node;
        this.weight = weight;
    }
}

public class DijkstraShortestPath {
    public static int[] dijkstra(int n, List<List<Pair>> graph, int src) {
        int[] dist = new int[n];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[src] = 0;

        PriorityQueue<Pair> pq = new PriorityQueue<>((a, b) -> a.weight - b.weight);
        pq.offer(new Pair(src, 0));

        while (!pq.isEmpty()) {
            Pair current = pq.poll();
            int node = current.node;
            int d = current.weight;

            if (d > dist[node]) continue; // Skip outdated pair

            for (Pair neighbor : graph.get(node)) {
                int nextNode = neighbor.node;
                int weight = neighbor.weight;

                if (dist[node] + weight < dist[nextNode]) {
                    dist[nextNode] = dist[node] + weight;
                    pq.offer(new Pair(nextNode, dist[nextNode]));
                }
            }
        }

        return dist;
    }

    public static void main(String[] args) {
        int n = 5;
        List<List<Pair>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

        // Directed or undirected graph with weights
        graph.get(0).add(new Pair(1, 2));
        graph.get(0).add(new Pair(2, 4));
        graph.get(1).add(new Pair(2, 1));
        graph.get(1).add(new Pair(3, 7));
        graph.get(2).add(new Pair(4, 3));
        graph.get(3).add(new Pair(4, 1));

        int[] dist = dijkstra(n, graph, 0);
        System.out.println("Shortest distances from 0: " + Arrays.toString(dist));
    }
}
```

---

### ✅ Output

```
Shortest distances from 0: [0, 2, 3, 9, 6]
```

---

### 🧰 Optional: Reconstructing Path

Add a `parent[]` array:

```java
int[] parent = new int[n];
Arrays.fill(parent, -1);
...
parent[nextNode] = node;
```

To reconstruct the path from `src` to `dest`, backtrack from `dest` using `parent[]`.

---

### 🧠 Why Dijkstra Works

- Each node is processed only after the **shortest distance to it is finalized**.
    
- PriorityQueue ensures the next node with the **lowest distance** is always picked.
    

---

### ✅ Summary Table

|Feature|Dijkstra|
|---|---|
|Graph Type|Directed/Undirected|
|Edge Weights|Non-negative only|
|Time Complexity|O((V + E) log V)|
|Supports Path Reconstruction|Yes (with parent array)|
|Handles Negative Weights|❌ No|

---

### 🔁 Related Algorithms

|Problem|Algorithm|
|---|---|
|Negative weights|Bellman-Ford|
|Unweighted graphs|BFS|
|Multiple sources|Dijkstra from each|
|Grid problems with weights|Dijkstra on matrix|
|K-shortest paths / path count|Dijkstra + DP/Heap|

---

Let me know if you want:

- **Path reconstruction**
    
- **Grid-based Dijkstra**
    
- **Bellman-Ford notes**
    
- **Fibonacci heap variant (for O(E + V log V))**
    
- **Comparison with A***