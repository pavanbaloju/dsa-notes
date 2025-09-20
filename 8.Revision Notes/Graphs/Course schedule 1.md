Here are **full, clean, and structured notes for Course Schedule I (Leetcode 207)** using **both DFS (Graph Coloring)** and **BFS (Kahn’s Algorithm)** approaches:

---

# ✅ Course Schedule I – Full Notes (DFS & BFS)

---

## 🧾 Problem Summary

You are given:

- An integer `numCourses` representing the number of courses.
    
- A list of prerequisite pairs `prerequisites`, where `prerequisites[i] = [a, b]` means **to take course `a`, you must first take course `b`**.
    

**Return `true` if it is possible to finish all courses. Otherwise, return `false`.**

---

## 🧠 Core Idea

Courses and their prerequisites can be represented as a **Directed Graph**:

- Each course is a node.
    
- Each prerequisite pair `[a, b]` adds an edge `b → a`.
    

The task reduces to checking if the **directed graph is acyclic**:

- If there is a **cycle**, the course schedule **cannot be completed**.
    
- If there is **no cycle**, it **can be completed**.
    

---

## 🔍 Approach 1: **DFS + Graph Coloring** (Cycle Detection)

### 🎨 States:

We color each node (course) as:

- `0` → **Unvisited**
    
- `1` → **Visiting (in recursion stack)**
    
- `2` → **Visited (fully explored)**
    

### 🔁 DFS Logic:

- If you reach a neighbor in **state 1**, a **cycle** is detected (back edge).
    
- If neighbor is in **state 0**, recursively DFS.
    
- After processing all neighbors, mark the node as **visited (2)**.
    

---

### ✅ Java Code – DFS + Graph Coloring

```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        // Step 1: Build the adjacency list
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < numCourses; i++)
            graph.add(new ArrayList<>());

        for (int[] pair : prerequisites) {
            graph.get(pair[1]).add(pair[0]); // edge: b → a
        }

        int[] state = new int[numCourses]; // 0 = unvisited, 1 = visiting, 2 = visited

        for (int i = 0; i < numCourses; i++) {
            if (state[i] == 0 && hasCycle(graph, state, i))
                return false;
        }

        return true;
    }

    private boolean hasCycle(List<List<Integer>> graph, int[] state, int node) {
        state[node] = 1; // mark as visiting

        for (int neighbor : graph.get(node)) {
            if (state[neighbor] == 1) return true; // cycle
            if (state[neighbor] == 0 && hasCycle(graph, state, neighbor))
                return true;
        }

        state[node] = 2; // mark as visited
        return false;
    }
}
```

---

### ⏱ Time and Space Complexity (DFS)

- **Time**: `O(V + E)`
    
- **Space**: `O(V + E)` for graph + `O(V)` for state + call stack
    

---

## 🔁 Approach 2: **BFS + Kahn’s Algorithm** (Topological Sort)

### 🔧 Key Idea:

Use **in-degree** (number of prerequisites for each course):

- Add all nodes with `in-degree == 0` to queue (no prerequisites).
    
- Process them one by one:
    
    - For each course taken, reduce the in-degree of dependent courses.
        
    - If a course’s in-degree becomes `0`, add it to queue.
        

If all nodes are processed → **no cycle**  
If some nodes remain unprocessed → **cycle exists**

---

### ✅ Java Code – BFS (Kahn’s Algorithm)

```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        int[] inDegree = new int[numCourses];
        List<List<Integer>> graph = new ArrayList<>();

        for (int i = 0; i < numCourses; i++)
            graph.add(new ArrayList<>());

        for (int[] pair : prerequisites) {
            graph.get(pair[1]).add(pair[0]);
            inDegree[pair[0]]++; // a depends on b → increase in-degree of a
        }

        Queue<Integer> queue = new LinkedList<>();

        for (int i = 0; i < numCourses; i++) {
            if (inDegree[i] == 0)
                queue.offer(i);
        }

        int processed = 0;

        while (!queue.isEmpty()) {
            int course = queue.poll();
            processed++;

            for (int neighbor : graph.get(course)) {
                inDegree[neighbor]--;
                if (inDegree[neighbor] == 0)
                    queue.offer(neighbor);
            }
        }

        return processed == numCourses;
    }
}
```

---

### ⏱ Time and Space Complexity (BFS)

- **Time**: `O(V + E)`
    
- **Space**: `O(V + E)` for graph + queue + in-degree
    

---

## ⚖️ DFS vs BFS

|Feature|DFS (Coloring)|BFS (Kahn’s Algo)|
|---|---|---|
|Detects cycle|✅ Yes|✅ Yes|
|Uses stack/recursion|✅ Yes (recursive)|❌ No|
|Gives topo order|❌ No|✅ Yes (can be extended)|
|Better for|Early cycle detection|Course ordering / parallel jobs|
|Can overflow stack|⚠️ Yes (deep graphs)|❌ No|

---

## 🔥 Interview Tips

- **Mention both approaches**. Use DFS if they ask for “can it be completed?” and BFS if they ask for the **order of completion** (topo sort).
    
- Be careful with **edge direction** → `b → a` means `a` depends on `b`.
    
- Avoid revisiting visited nodes in DFS to prevent TLE.
    

---

## 🧩 Related Variants

|Problem|Variation|
|---|---|
|Course Schedule II (LC 210)|Return actual order|
|Alien Dictionary|Topo sort on unknown alphabet|
|Find Eventual Safe States (LC 802)|Terminal nodes in DAG|
|Minimum Semesters to Complete Courses|BFS with levels (layered topological)|

---

Would you like these notes in a printable markdown or PDF format?