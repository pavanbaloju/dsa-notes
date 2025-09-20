Let's go through **Leetcode 841. Keys and Rooms** with a complete explanation and BFS/DFS-based solutions.

---

## 🧩 Problem Summary

You are given an array `rooms` where `rooms[i]` is a list of keys in room `i`.  
You start in room 0.  
Each key in a room allows you to enter another room.

**Goal:** Return `true` if you can visit **all** the rooms, otherwise return `false`.

---

## 🔧 Constraints

- The graph is **directed**.
    
- You are given a **list of lists**.
    
- Room 0 is **unlocked**.
    
- Number of rooms = `n`, where `1 <= n <= 1000`
    

---

## ✅ Intuition

We can model this as a **graph traversal** problem:

- Each room is a **node**
    
- Each key is a **directed edge** to another node
    

We start at room 0 and want to **visit all nodes** using keys.

This is a classic **graph reachability** problem.

---

## ✅ Approach 1: DFS (Depth-First Search)

### 🔄 Idea

- Start from room 0
    
- Mark it visited
    
- For each key in the room, if the room is not visited, recursively visit it
    

### ✅ Code

```java
class Solution {
    public boolean canVisitAllRooms(List<List<Integer>> rooms) {
        boolean[] visited = new boolean[rooms.size()];
        dfs(0, rooms, visited);

        for (boolean roomVisited : visited) {
            if (!roomVisited) return false;
        }
        return true;
    }

    private void dfs(int room, List<List<Integer>> rooms, boolean[] visited) {
        visited[room] = true;

        for (int key : rooms.get(room)) {
            if (!visited[key]) {
                dfs(key, rooms, visited);
            }
        }
    }
}
```

---

## ✅ Approach 2: BFS (Breadth-First Search)

### 🔄 Idea

- Use a queue to simulate level-order visiting of rooms
    
- Track visited rooms with a boolean array
    
- Enqueue all unvisited rooms we find keys for
    

### ✅ Code

```java
class Solution {
    public boolean canVisitAllRooms(List<List<Integer>> rooms) {
        int n = rooms.size();
        boolean[] visited = new boolean[n];
        Queue<Integer> queue = new LinkedList<>();

        queue.offer(0);
        visited[0] = true;

        while (!queue.isEmpty()) {
            int room = queue.poll();

            for (int key : rooms.get(room)) {
                if (!visited[key]) {
                    visited[key] = true;
                    queue.offer(key);
                }
            }
        }

        for (boolean roomVisited : visited) {
            if (!roomVisited) return false;
        }

        return true;
    }
}
```

---

## 🧠 Complexity Analysis

|Measure|Value|
|---|---|
|Time|O(N + E), where N = number of rooms, E = total number of keys|
|Space|O(N) for visited array and recursion stack or queue|

---

## 🧪 Example

```java
Input: [[1], [2], [3], []]
Output: true

// Room 0 → has key 1 → room 1 → has key 2 → room 2 → has key 3 → room 3 → done
```

---

## 🔍 Summary

|Variant|Key Idea|Pros|
|---|---|---|
|DFS|Recursively visit rooms|Easy to implement|
|BFS|Queue-based level visiting|Can be more intuitive for shortest path|

---

Let me know if you'd like to visualize this with a graph, or try more problems like this (graph traversal, reachability, etc).