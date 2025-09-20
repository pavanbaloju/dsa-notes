Here are the **full notes on solving "Evaluate Division" using BFS**, including the problem breakdown, graph construction, BFS traversal, Java code with comments, and key insights.

---

## ✅ Problem: Evaluate Division (Leetcode 399)

You're given:

- A list of equations like `["a", "b"]` representing `a / b = k`
    
- A list of values like `[2.0]` meaning `a / b = 2.0`
    
- A list of queries like `["a", "c"]`
    

Return results for each query — if the answer can't be determined, return `-1.0`.

---

## ✅ BFS Solution: Intuition

Treat each variable as a **node** and each equation as a **bidirectional weighted edge**.

- From `a -> b`, store weight `k`
    
- From `b -> a`, store weight `1/k`
    

Then for each query `start / end`, do a **Breadth-First Search (BFS)** starting at `start`:

- Multiply the edge weights as you traverse
    
- If you reach `end`, return the product
    
- If `end` is unreachable, return `-1.0`
    

---

## ✅ Graph Representation

```text
a / b = 2.0  ➝  a → b (2.0), b → a (0.5)
b / c = 3.0  ➝  b → c (3.0), c → b (1/3.0)
```

---

## ✅ Java Code (with Comments)

```java
import java.util.*;

public class EvaluateDivisionBFS {

    public double[] calcEquation(List<List<String>> equations, double[] values, List<List<String>> queries) {
        // Step 1: Build the graph
        Map<String, Map<String, Double>> graph = new HashMap<>();

        for (int i = 0; i < equations.size(); i++) {
            String u = equations.get(i).get(0);
            String v = equations.get(i).get(1);
            double val = values[i];

            graph.putIfAbsent(u, new HashMap<>());
            graph.putIfAbsent(v, new HashMap<>());

            graph.get(u).put(v, val);
            graph.get(v).put(u, 1.0 / val);
        }

        // Step 2: Process queries using BFS
        double[] results = new double[queries.size()];

        for (int i = 0; i < queries.size(); i++) {
            String src = queries.get(i).get(0);
            String dest = queries.get(i).get(1);

            if (!graph.containsKey(src) || !graph.containsKey(dest)) {
                results[i] = -1.0;
            } else if (src.equals(dest)) {
                results[i] = 1.0;
            } else {
                results[i] = bfs(graph, src, dest);
            }
        }

        return results;
    }

    private double bfs(Map<String, Map<String, Double>> graph, String src, String dest) {
        Queue<Pair> queue = new LinkedList<>();
        Set<String> visited = new HashSet<>();

        queue.offer(new Pair(src, 1.0));
        visited.add(src);

        while (!queue.isEmpty()) {
            Pair current = queue.poll();
            String node = current.var;
            double product = current.product;

            if (node.equals(dest)) {
                return product;
            }

            for (Map.Entry<String, Double> neighbor : graph.get(node).entrySet()) {
                if (!visited.contains(neighbor.getKey())) {
                    visited.add(neighbor.getKey());
                    queue.offer(new Pair(neighbor.getKey(), product * neighbor.getValue()));
                }
            }
        }

        return -1.0;
    }

    private static class Pair {
        String var;
        double product;

        public Pair(String var, double product) {
            this.var = var;
            this.product = product;
        }
    }
}
```

---

## ✅ BFS vs DFS

|Feature|BFS|DFS|
|---|---|---|
|Strategy|Level-by-level search|Depth-first traversal|
|Early termination|Yes, can return immediately on match|Also possible but can go deeper first|
|Space Complexity|Can be higher (queue)|Recursion stack (can overflow)|
|Suitable for|Shortest path-type problems|Exploring all paths / backtracking|

Both work fine here; BFS avoids recursion and can be easier to manage in some environments.

---

## ✅ Time & Space Complexity

Let:

- `n = number of variables`
    
- `m = number of equations`
    
- `q = number of queries`
    

**Time Complexity:**

- Graph build: `O(m)`
    
- Each query BFS: `O(n)` in worst case
    
- Total: `O(m + qn)`
    

**Space Complexity:**

- Graph: `O(m)`
    
- BFS queue/visited: `O(n)`
    

---

## ✅ Sample Example

**Equations:**

```
a / b = 2.0  
b / c = 3.0
```

**Graph:**

```
a → b (2.0)  
b → a (0.5)  
b → c (3.0)  
c → b (1/3.0)
```

**Query:** `a / c`

- BFS: `a → b (2.0) → c (3.0)`
    
- Answer: `2.0 * 3.0 = 6.0`
    

---

## ✅ Interview Tips

- Mention you're modeling a graph with bidirectional edges and weighted values.
    
- Always clarify edge cases:
    
    - Division by self (like `a / a`)
        
    - Missing variables
        
- Explain why you chose BFS (early exit, iterative, memory safe).
    

---

Would you like the **Union-Find with weighted path compression** version as well? It's a more advanced version for bulk queries.