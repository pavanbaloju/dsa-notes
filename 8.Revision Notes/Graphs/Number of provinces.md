 Here's the **complete guide to solving "Number of Provinces" (Leetcode 547)** — with explanation, code, dry run intuition, and time/space analysis.

---

## 🔍 Problem Statement

You are given a `n x n` matrix `isConnected`, where:

- `isConnected[i][j] == 1` means city `i` and city `j` are directly connected.
    
- `isConnected[i][j] == 0` means no direct connection.
    

A **province** is a group of directly or indirectly connected cities.

**Goal:** Return the total number of provinces (i.e., number of connected components in the graph).

---

## ✅ Input / Output

### Input:

```java
isConnected = {
  {1,1,0},
  {1,1,0},
  {0,0,1}
}
```

### Output:

```
2
```

Explanation: There are two provinces — one with cities 0 and 1, and one with city 2.

---

## 🧠 Intuition

The matrix `isConnected` is an **adjacency matrix of an undirected graph**.

Each province corresponds to a **connected component** in this graph.

---

## ✅ Approaches

### 🔹 Approach 1: DFS

- Traverse the graph using DFS.
    
- Count how many times you initiate DFS — that gives you the number of provinces.
    

---

### ✅ Java Code (DFS)

```java
class Solution {
    public int findCircleNum(int[][] isConnected) {
        int n = isConnected.length;
        boolean[] visited = new boolean[n];
        int count = 0;

        for (int city = 0; city < n; city++) {
            if (!visited[city]) {
                dfs(city, isConnected, visited);
                count++; // finished one connected component
            }
        }

        return count;
    }

    private void dfs(int curr, int[][] isConnected, boolean[] visited) {
        visited[curr] = true;

        for (int neighbor = 0; neighbor < isConnected.length; neighbor++) {
            if (isConnected[curr][neighbor] == 1 && !visited[neighbor]) {
                dfs(neighbor, isConnected, visited);
            }
        }
    }
}
```

---

## 🔁 Dry Run

Using:

```java
isConnected = {
  {1,1,0},
  {1,1,0},
  {0,0,1}
}
```

- Start at city 0:
    
    - DFS to 1 (since 0 → 1 connected)
        
    - DFS finishes → count = 1
        
- City 1 already visited.
    
- City 2 not visited:
    
    - DFS from 2 (no neighbors)
        
    - count = 2
        

---

## 📊 Time and Space Complexity

|Metric|Value|
|---|---|
|Time|O(n²)|
|Space|O(n) for `visited` + O(n) recursion stack|

---

## 🔹 Approach 2: Union-Find (Disjoint Set Union)

- Initialize `n` disjoint sets (each city is its own province).
    
- For each `isConnected[i][j] == 1`, union `i` and `j`.
    
- Final number of unique parents = number of provinces.
    

👉 Let me know if you want Union-Find version with path compression!

---

## ✅ Summary Table

|Feature|DFS Approach|
|---|---|
|Type|Graph traversal|
|Traversal technique|DFS|
|When to use|Adjacency matrix|
|Space usage|O(n)|
|Time|O(n²)|
|Handles disconnected|Yes (that's the goal)|
|Number of DFS calls|Equals province count|

---

Let me know if you'd like the **BFS version**, **Union-Find**, or to **visualize the traversal**.