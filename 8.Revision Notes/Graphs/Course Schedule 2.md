Here are the **full notes for Course Schedule II (Leetcode 210)** using both:

---

### ✅ Problem Summary

You're given `numCourses` courses labeled from `0` to `numCourses - 1` and a list of prerequisites such that `prerequisites[i] = [a, b]` means to take course `a`, you must have completed course `b`.

Return **any valid ordering** of courses such that prerequisites are satisfied. If not possible (cycle exists), return an empty array.

---

## ✅ Approach 1: DFS + Stack (Topological Sort using Post-order)

### 🔍 Intuition

- Model the courses as a **Directed Graph**.
    
- Use **DFS traversal**.
    
- When a node finishes visiting all its dependencies, **push it to a stack**.
    
- If we detect a **cycle** (node visited while still on the current path), return `[]`.
    

### 🧠 Key Concepts

- **Visited state array**:
    
    - `0`: unvisited
        
    - `1`: visiting (currently in recursion stack)
        
    - `2`: visited (completely processed)
        
- Post-order traversal to push nodes onto stack **after all dependencies** are resolved.
    

---

### ✅ Java Code (DFS + Stack)

```java
public class CourseSchedule2DFS {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < numCourses; i++) graph.add(new ArrayList<>());
        
        // Build graph: edge from b -> a
        for (int[] pre : prerequisites)
            graph.get(pre[1]).add(pre[0]);

        int[] state = new int[numCourses]; // 0 = unvisited, 1 = visiting, 2 = visited
        Stack<Integer> stack = new Stack<>();

        for (int i = 0; i < numCourses; i++) {
            if (state[i] == 0 && hasCycle(i, graph, state, stack)) {
                return new int[0]; // cycle found
            }
        }

        // Convert stack to array (reverse post-order)
        int[] result = new int[numCourses];
        for (int i = 0; i < numCourses; i++)
            result[i] = stack.pop();

        return result;
    }

    private boolean hasCycle(int node, List<List<Integer>> graph, int[] state, Stack<Integer> stack) {
        state[node] = 1; // mark as visiting

        for (int neighbor : graph.get(node)) {
            if (state[neighbor] == 1) return true; // back edge → cycle
            if (state[neighbor] == 0 && hasCycle(neighbor, graph, state, stack))
                return true;
        }

        state[node] = 2; // mark as visited
        stack.push(node); // all dependencies resolved
        return false;
    }
}
```

---

### ✅ Time and Space Complexity

- **Time:** `O(V + E)` where `V = numCourses`, `E = prerequisites.length`
    
- **Space:** `O(V + E)` for graph + state + recursion + stack
    

---

## ✅ Approach 2: Kahn’s Algorithm (BFS + Queue/Stack)

### 🔍 Intuition

- Track the number of prerequisites (indegree) for each course.
    
- Start with nodes having `indegree == 0`.
    
- As you take a course, reduce indegree of its neighbors.
    
- If any neighbor reaches indegree 0, it becomes available.
    

### 🧠 Why it works?

- Ensures no course is taken before its prerequisites.
    
- If at the end, all nodes are processed → valid order exists.
    
- If not all courses are added → there's a cycle.
    

---

### ✅ Java Code (BFS - Kahn’s Algorithm with Queue)

```java
public class CourseSchedule2BFS {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        List<List<Integer>> graph = new ArrayList<>();
        int[] indegree = new int[numCourses];

        for (int i = 0; i < numCourses; i++) graph.add(new ArrayList<>());
        for (int[] pre : prerequisites) {
            graph.get(pre[1]).add(pre[0]);
            indegree[pre[0]]++;
        }

        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < numCourses; i++)
            if (indegree[i] == 0) queue.offer(i);

        int[] result = new int[numCourses];
        int idx = 0;

        while (!queue.isEmpty()) {
            int course = queue.poll();
            result[idx++] = course;

            for (int neighbor : graph.get(course)) {
                indegree[neighbor]--;
                if (indegree[neighbor] == 0) queue.offer(neighbor);
            }
        }

        return idx == numCourses ? result : new int[0];
    }
}
```

---

### ✅ Java Code (BFS with Stack for different valid order)

```java
public class CourseSchedule2BFSStack {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        List<List<Integer>> graph = new ArrayList<>();
        int[] indegree = new int[numCourses];

        for (int i = 0; i < numCourses; i++) graph.add(new ArrayList<>());
        for (int[] pre : prerequisites) {
            graph.get(pre[1]).add(pre[0]);
            indegree[pre[0]]++;
        }

        Stack<Integer> stack = new Stack<>();
        for (int i = 0; i < numCourses; i++)
            if (indegree[i] == 0) stack.push(i);

        int[] result = new int[numCourses];
        int idx = 0;

        while (!stack.isEmpty()) {
            int course = stack.pop();
            result[idx++] = course;

            for (int neighbor : graph.get(course)) {
                indegree[neighbor]--;
                if (indegree[neighbor] == 0)
                    stack.push(neighbor);
            }
        }

        return idx == numCourses ? result : new int[0];
    }
}
```

---

### ✅ Time and Space Complexity (BFS)

- **Time:** `O(V + E)`
    
- **Space:** `O(V + E)` for graph + indegree + queue
    

---

## ✅ When to Use Which?

|Approach|Pros|Cons|
|---|---|---|
|DFS + Stack|Simpler to implement recursively|Harder to detect cycles without state tracking|
|Kahn’s BFS|Very intuitive for course planning|Slightly more code for indegree handling|

---

## ✅ Dry Run Example

For `numCourses = 4`, `prerequisites = [[1,0],[2,0],[3,1],[3,2]]`:

- `0 → 1`, `0 → 2`, `1 → 3`, `2 → 3`
    
- Valid orders: `[0,2,1,3]`, `[0,1,2,3]`, etc.
    

Both approaches will return one of the valid topological sorts.

---

Let me know if you want to include **cycle visualization**, **tracing** for a test case, or convert to **Python**.