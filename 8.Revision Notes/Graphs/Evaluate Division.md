Here's a complete breakdown of the **Leetcode 399: Evaluate Division** problem — it's a great application of graphs in disguise.

---

## 🔍 Problem: [Evaluate Division](https://leetcode.com/problems/evaluate-division/)

You are given:

- A list of equations like `a / b = 2.0`
    
- A list of queries like `a / c = ?`
    

Return the result of each query. If the answer does not exist, return `-1.0`.

---

## 🧠 Intuition

Treat each variable as a **node** in a graph.  
Each equation `a / b = 2.0` becomes a **directed edge** from:

- `a` to `b` with weight `2.0`
    
- and **also** from `b` to `a` with weight `1/2.0`
    

The task is to answer queries by **finding the path from the numerator to the denominator** and multiplying the weights along that path.

---

## 🧱 Graph Construction

Use a **HashMap<String, Map<String, Double>>**  
Each key is a node; value is a map of neighbors and weights.

Example:

```java
equations = [["a", "b"], ["b", "c"]]
values = [2.0, 3.0]
```

Becomes:

```
a -> { b: 2.0 }
b -> { a: 0.5, c: 3.0 }
c -> { b: 1/3.0 }
```

---

## ✅ Approach

1. **Build graph** from equations and values
    
2. For each query:
    
    - If source or target not in graph, return -1.0
        
    - Else, use **DFS/BFS** to find path from source to target and compute product of weights
        
3. Return results for all queries
    

---

## ✅ Java Code (DFS)

```java
public class Solution {

    public double[] calcEquation(List<List<String>> equations, double[] values, List<List<String>> queries) {
        Map<String, Map<String, Double>> graph = new HashMap<>();

        // Step 1: Build the graph
        for (int i = 0; i < equations.size(); i++) {
            String u = equations.get(i).get(0);
            String v = equations.get(i).get(1);
            double val = values[i];

            graph.putIfAbsent(u, new HashMap<>());
            graph.putIfAbsent(v, new HashMap<>());

            graph.get(u).put(v, val);
            graph.get(v).put(u, 1.0 / val);
        }

        // Step 2: Evaluate each query using DFS
        double[] result = new double[queries.size()];
        for (int i = 0; i < queries.size(); i++) {
            String src = queries.get(i).get(0);
            String dest = queries.get(i).get(1);

            if (!graph.containsKey(src) || !graph.containsKey(dest)) {
                result[i] = -1.0;
            } else if (src.equals(dest)) {
                result[i] = 1.0;
            } else {
                Set<String> visited = new HashSet<>();
                result[i] = dfs(graph, src, dest, 1.0, visited);
            }
        }

        return result;
    }

    private double dfs(Map<String, Map<String, Double>> graph, String curr, String target, double product, Set<String> visited) {
        if (curr.equals(target)) return product;

        visited.add(curr);

        for (Map.Entry<String, Double> neighbor : graph.get(curr).entrySet()) {
            String next = neighbor.getKey();
            double val = neighbor.getValue();

            if (!visited.contains(next)) {
                double result = dfs(graph, next, target, product * val, visited);
                if (result != -1.0) return result;
            }
        }

        return -1.0;
    }
}
```

---
## ✅ Java Code (BFS)

```java
public class Solution {
    public double[] calcEquation(
        List<List<String>> equations,
        double[] values,
        List<List<String>> queries
    ) {
        Map<String, Map<String, Double>> graph = buildGraph(equations, values);
        double[] results = new double[queries.size()];

        for (int i = 0; i < queries.size(); i++) {
            String start = queries.get(i).get(0);
            String end = queries.get(i).get(1);
            results[i] = bfs(start, end, graph);
        }

        return results;
    }

    // Build graph as adjacency list
    private Map<String, Map<String, Double>> buildGraph(List<List<String>> equations, double[] values) {
        Map<String, Map<String, Double>> graph = new HashMap<>();

        for (int i = 0; i < equations.size(); i++) {
            String u = equations.get(i).get(0);
            String v = equations.get(i).get(1);
            double w = values[i];

            graph.putIfAbsent(u, new HashMap<>());
            graph.putIfAbsent(v, new HashMap<>());

            graph.get(u).put(v, w);
            graph.get(v).put(u, 1.0 / w);
        }

        return graph;
    }

    // BFS traversal to compute value of start / end
    private double bfs(String start, String end, Map<String, Map<String, Double>> graph) {
        if (!graph.containsKey(start) || !graph.containsKey(end)) return -1.0;
        if (start.equals(end)) return 1.0;

        Queue<Pair<String, Double>> queue = new LinkedList<>();
        Set<String> visited = new HashSet<>();

        queue.offer(new Pair<>(start, 1.0));
        visited.add(start);

        while (!queue.isEmpty()) {
            Pair<String, Double> curr = queue.poll();
            String node = curr.getKey();
            double prod = curr.getValue();

            if (node.equals(end)) return prod;

            for (Map.Entry<String, Double> neighbor : graph.get(node).entrySet()) {
                String next = neighbor.getKey();
                double weight = neighbor.getValue();

                if (!visited.contains(next)) {
                    visited.add(next);
                    queue.offer(new Pair<>(next, prod * weight));
                }
            }
        }

        return -1.0; // no path found
    }
}

```

## 🧠 Dry Run

### Input:

```java
equations = [["a","b"],["b","c"]]
values = [2.0,3.0]
queries = [["a","c"],["b","a"],["a","e"],["a","a"],["x","x"]]
```

### Output:

```
[6.0, 0.5, -1.0, 1.0, -1.0]
```

---

## ⏱️ Time and Space Complexity

- Time: O(Q * E) where Q = number of queries, E = edges in graph
    
- Space: O(N) for graph and visited set
    

---

## 🧩 Related Variants

- Similar to **Path with Product**
    
- Problems like evaluating formulas, currencies, or exchange rates
    

---

Would you like the **BFS version**, **Union-Find approach**, or a **diagram-based visual explanation**?