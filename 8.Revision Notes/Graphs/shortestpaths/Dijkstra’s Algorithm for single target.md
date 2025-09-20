Here’s a full breakdown of **Dijkstra’s Algorithm for finding the shortest path from a single source to a single target** — optimized for early termination.

---

## ✅ Use Case

- Graph is **weighted** and **non-negative**.
    
- You need the **shortest distance** (and optionally, the path) from **source node `S` to a target node `T`**, **not all nodes**.
    

---

## 🚀 Optimization over full Dijkstra

In regular Dijkstra (single-source to all-nodes), we process the entire graph.  
But if you only need to reach **one target node**, you can **terminate as soon as you pop the target** from the priority queue — this guarantees that you've found the shortest path to it.

---

## 🧠 Why is that safe?

Because the node you pop from the **min-heap** is guaranteed to be the one with the smallest distance found so far. So the **first time you pop the target node**, it must be via the shortest path.

---

## 📋 Step-by-step Algorithm

1. Create a **min-heap** (priority queue): `(distance_so_far, node)`.
    
2. Initialize `dist[]` array with `∞` (or `Integer.MAX_VALUE` in Java).
    
3. Set `dist[source] = 0` and push `(0, source)` into the heap.
    
4. While heap is not empty:
    
    - Pop `(d, node)` from heap.
        
    - If `node == target`, return `d` (shortest path found).
        
    - If `d > dist[node]`, skip (stale entry).
        
    - For each neighbor:
        
        - If a shorter distance is found, update and push into heap.
            

---

## 🧮 Time & Space Complexity

- **Time:** O((V + E) log V) in general, but stops early once `T` is reached.
    
- **Space:** O(V) for `dist[]`, O(E) for graph, O(V) for heap.
    

---

## ✅ Java Implementation (Distance Only)

```java
import java.util.*;

public class DijkstraSingleTarget {
    static class Pair {
        int node, weight;
        Pair(int n, int w) {
            node = n; weight = w;
        }
    }

    public int dijkstra(int n, List<List<Pair>> graph, int source, int target) {
        int[] dist = new int[n];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[source] = 0;

        PriorityQueue<int[]> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a[0]));
        pq.offer(new int[]{0, source});

        while (!pq.isEmpty()) {
            int[] curr = pq.poll();
            int d = curr[0], node = curr[1];

            if (node == target) return d; // early exit

            if (d > dist[node]) continue;

            for (Pair neighbor : graph.get(node)) {
                int next = neighbor.node;
                int cost = neighbor.weight;

                if (dist[node] + cost < dist[next]) {
                    dist[next] = dist[node] + cost;
                    pq.offer(new int[]{dist[next], next});
                }
            }
        }

        return -1; // target unreachable
    }
}
```

---

## 🔁 With Path Reconstruction

To find the actual **path from source to target**, maintain a `parent[]` array.

### Changes:

- Add `int[] parent = new int[n];`
    
- Update parent when distance improves.
    
- After Dijkstra finishes, reconstruct path by backtracking from `target`.
    

```java
// Inside loop
if (dist[node] + cost < dist[next]) {
    dist[next] = dist[node] + cost;
    parent[next] = node;
    pq.offer(new int[]{dist[next], next});
}
```

```java
// After exiting Dijkstra
List<Integer> path = new ArrayList<>();
for (int at = target; at != source; at = parent[at]) {
    path.add(at);
}
path.add(source);
Collections.reverse(path);
```

---

## 📦 Graph Input Format

The graph is stored as:

```java
List<List<Pair>> graph = new ArrayList<>();
for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

// Add edges
graph.get(u).add(new Pair(v, weight));
```

---

## 🧪 Example

```java
n = 5
Edges:
0 -> 1 (2)
0 -> 2 (4)
1 -> 2 (1)
1 -> 3 (7)
2 -> 4 (3)
3 -> 4 (1)

source = 0, target = 4
Output: 6 (0 → 1 → 2 → 4)
```

---

## ✅ Summary

|Feature|Dijkstra for Single Target|
|---|---|
|Graph Type|Weighted, Directed/Undirected|
|Edge Weights|Non-negative|
|Termination|When target is popped from heap|
|Best For|Early exit when only one destination matters|
|Time|Up to `O((V + E) log V)` but stops earlier|
|Space|O(V + E)|

---

Want the same for **Bidirectional Dijkstra**, **A***, or **grid-based version to single target**?