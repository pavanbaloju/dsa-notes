To find the **shortest path from source to destination** in an **unweighted graph**, along with the **path itself**, you can enhance the BFS algorithm by keeping a `parent[]` array to trace the path back once the destination is found.

---

## ✅ Full Java Code: BFS for Single Source Shortest Path + Path Reconstruction

```java
import java.util.*;

public class ShortestPathWithTrace {
    public static List<Integer> shortestPath(int n, List<List<Integer>> graph, int src, int dest) {
        boolean[] visited = new boolean[n];
        int[] parent = new int[n];       // To trace the path
        int[] distance = new int[n];     // Distance from src
        Arrays.fill(parent, -1);

        Queue<Integer> queue = new LinkedList<>();
        queue.offer(src);
        visited[src] = true;
        distance[src] = 0;

        while (!queue.isEmpty()) {
            int node = queue.poll();

            if (node == dest) break;  // Early stop once we reach destination

            for (int neighbor : graph.get(node)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    distance[neighbor] = distance[node] + 1;
                    parent[neighbor] = node;
                    queue.offer(neighbor);
                }
            }
        }

        // Reconstruct path
        List<Integer> path = new ArrayList<>();
        if (!visited[dest]) return path;  // No path found

        for (int at = dest; at != -1; at = parent[at]) {
            path.add(at);
        }
        Collections.reverse(path);

        return path;
    }

    public static void main(String[] args) {
        int n = 6;
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

        // Edges of undirected graph
        graph.get(0).add(1); graph.get(1).add(0);
        graph.get(0).add(2); graph.get(2).add(0);
        graph.get(1).add(3); graph.get(3).add(1);
        graph.get(2).add(4); graph.get(4).add(2);
        graph.get(4).add(5); graph.get(5).add(4);

        int src = 0, dest = 5;

        List<Integer> path = shortestPath(n, graph, src, dest);
        if (path.isEmpty()) {
            System.out.println("No path found from " + src + " to " + dest);
        } else {
            System.out.println("Shortest path from " + src + " to " + dest + ": " + path);
            System.out.println("Length: " + (path.size() - 1));
        }
    }
}
```

---

## ✅ Output

```
Shortest path from 0 to 5: [0, 2, 4, 5]
Length: 3
```

---

## ✅ Key Components

|Component|Role|
|---|---|
|`distance[]`|Stores shortest distance from source|
|`parent[]`|Tracks the predecessor of each node for path building|
|`visited[]`|Avoids revisiting nodes|
|`queue`|For BFS traversal|

---

## ✅ Summary

- Works perfectly for **unweighted** graphs (undirected or directed).
    
- You can also easily adapt this for **grid-based BFS** by treating cells as nodes.
    
- **Early exit** as soon as you reach `dest` makes it faster than BFS for all nodes when only one path is needed.
    

---

Let me know if you want:

- A **grid version** of this (for maze or matrix pathfinding),
    
- A **Dijkstra version** (for weighted graphs),
    
- A **bidirectional BFS** version (for large graphs with far source and dest).