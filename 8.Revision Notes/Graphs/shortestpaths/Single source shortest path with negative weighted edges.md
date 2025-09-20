Here's the **full explanation and code notes for Bellman-Ford Algorithm**, which handles graphs with **negative weights** and detects **negative weight cycles**.

---

## 🔍 Problem: Single Source Shortest Path (with Negative Weights)

Given a **directed graph** with `V` vertices and `E` edges, and a source vertex `src`, find the shortest path from `src` to all vertices. Also, detect if the graph contains any **negative weight cycle**.

---

## ✅ Why Bellman-Ford?

- Unlike Dijkstra’s algorithm, **Bellman-Ford works with negative weights**.
    
- It uses **edge relaxation**.
    
- It can detect **negative weight cycles**, which Dijkstra can't.
    

---

## 🧠 Intuition

- The shortest path in a graph with **V nodes** can have **at most V-1 edges**.
    
- So, we perform **V-1 iterations**, relaxing all edges each time.
    
- If we can still relax any edge on the **V-th iteration**, there’s a **negative weight cycle**.
    

---

## 📚 Time and Space Complexity

|Operation|Complexity|
|---|---|
|Time|O(V * E)|
|Space|O(V)|

---

## 🧾 Input

- `n`: Number of vertices (indexed from `0` to `n-1`)
    
- `edges`: List of edges as `int[][] edges` where each edge is `[u, v, weight]`
    
- `src`: Source node
    

---

## 🧩 Output

- Shortest distance from `src` to all other nodes.
    
- Or, report a negative weight cycle.
    

---

## 🧮 Algorithm Steps

1. **Initialize** distance array to `∞`, except for `src` which is 0.
    
2. **Relax all edges V - 1 times**.
    
3. **Check for negative cycles** with 1 more pass.
    

---

## ✅ Java Code with Comments

```java
public class BellmanFord {
    
    public static int[] bellmanFord(int n, int[][] edges, int src) {
        int[] dist = new int[n];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[src] = 0;

        // Step 1: Relax all edges V - 1 times
        for (int i = 0; i < n - 1; i++) {
            for (int[] edge : edges) {
                int u = edge[0];
                int v = edge[1];
                int weight = edge[2];
                if (dist[u] != Integer.MAX_VALUE && dist[u] + weight < dist[v]) {
                    dist[v] = dist[u] + weight;
                }
            }
        }

        // Step 2: Check for negative weight cycle
        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            int weight = edge[2];
            if (dist[u] != Integer.MAX_VALUE && dist[u] + weight < dist[v]) {
                throw new RuntimeException("Graph contains a negative weight cycle");
            }
        }

        return dist;
    }

    // Sample Usage
    public static void main(String[] args) {
        int n = 5;
        int[][] edges = {
            {0, 1, -1},
            {0, 2, 4},
            {1, 2, 3},
            {1, 3, 2},
            {1, 4, 2},
            {3, 2, 5},
            {3, 1, 1},
            {4, 3, -3}
        };

        int src = 0;

        try {
            int[] distances = bellmanFord(n, edges, src);
            for (int i = 0; i < distances.length; i++) {
                System.out.println("Distance to " + i + " = " + distances[i]);
            }
        } catch (RuntimeException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

---

## 🧠 When to Use Bellman-Ford?

- Graph may have **negative weight edges**
    
- You need to **detect a negative cycle**
    
- Works for **both directed and undirected** graphs (but negative cycles in undirected graphs usually create logical issues)
    

---

## 🧪 Edge Cases

- Negative weight cycle? → Detect using 1 extra iteration
    
- Disconnected nodes? → Their distances remain `Integer.MAX_VALUE`
    
- Large inputs? → O(V * E) can be slow
    

---

If you'd like the version that also returns the path (like a `parent[]` array), let me know.