Here's a complete and structured note on finding the **Single Source Shortest Path (SSSP) to a single target node** in an **unweighted graph**.

---

## 🔍 Problem Statement

 Given an **unweighted graph** and a source node `src`, find the **shortest path distance** from `src` to a given **target node** `dest`

---

## ✅ Approach: **BFS (Breadth-First Search)**

### 🔹 Why BFS?

- In unweighted graphs, all edges have the same "cost" (1).
    
- BFS explores level-by-level, guaranteeing the shortest path is found as soon as you reach the destination.
    

---

## ✅ Java Code – Distance to Single Target

```java
import java.util.*;

public class ShortestPathToTarget {
    public static int shortestPath(int n, List<List<Integer>> graph, int src, int dest) {
        boolean[] visited = new boolean[n];
        Queue<Integer> queue = new LinkedList<>();
        int[] distance = new int[n];  // distance[i] = min steps from src to i

        queue.offer(src);
        visited[src] = true;
        distance[src] = 0;

        while (!queue.isEmpty()) {
            int node = queue.poll();

            if (node == dest) {
                return distance[dest];  // Early exit when destination is reached
            }

            for (int neighbor : graph.get(node)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    distance[neighbor] = distance[node] + 1;
                    queue.offer(neighbor);
                }
            }
        }

        return -1;  // dest not reachable from src
    }

    public static void main(String[] args) {
        int n = 6;
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

        // Undirected edges
        graph.get(0).add(1); graph.get(1).add(0);
        graph.get(0).add(2); graph.get(2).add(0);
        graph.get(1).add(3); graph.get(3).add(1);
        graph.get(2).add(4); graph.get(4).add(2);
        graph.get(4).add(5); graph.get(5).add(4);

        int src = 0, dest = 5;
        int shortest = shortestPath(n, graph, src, dest);
        System.out.println("Shortest path from " + src + " to " + dest + ": " + shortest);
    }
}
```

---

## ✅ Time & Space Complexity

|Metric|Value|
|---|---|
|Time|`O(V + E)`|
|Space|`O(V)` (visited, distance, and queue)|

---

## ✅ BFS Template (for SSSP to a single node)

```java
queue.offer(start);
visited[start] = true;
distance[start] = 0;

while (!queue.isEmpty()) {
    node = queue.poll();

    if (node == target) return distance[node];  // EARLY EXIT

    for (neighbor : graph.get(node)) {
        if (!visited[neighbor]) {
            visited[neighbor] = true;
            distance[neighbor] = distance[node] + 1;
            queue.offer(neighbor);
        }
    }
}
```

---

## 🔁 What If You Want the Actual Path?

You can maintain a `parent[]` array:

- When you visit a neighbor, record: `parent[neighbor] = node`
- Once you reach `dest`, reconstruct the path backward

```java
List<Integer> path = new ArrayList<>();
for (int at = dest; at != -1; at = parent[at]) {
    path.add(at);
}
Collections.reverse(path);
```

---

## 🚫 When This Fails

- If graph is **weighted** → use **Dijkstra’s Algorithm**.
    
- If graph has **negative weights** → use **Bellman-Ford**.
    

---

## ✅ Summary

|Feature|BFS for SSSP to One Node|
|---|---|
|Works for Unweighted Graphs|✅ Yes|
|Stops as soon as target found|✅ Efficient|
|Time Complexity|`O(V + E)`|
|Best Use Case|Grid problems, basic graphs, word ladders, etc.|

---

Let me know if you want:

- Grid version (`int[][] grid`) for Maze-type problems
    
- Path reconstruction
    
- Weighted version (Dijkstra)
    
- JavaScript/Python version