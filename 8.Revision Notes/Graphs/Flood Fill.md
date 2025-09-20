Here are the **full updated notes for the Flood Fill algorithm**, including the fixed BFS approach, detailed explanation, code with comments, time & space complexity, and intuition.

---

## ✅ Flood Fill – Full Notes

**LeetCode #733: Flood Fill**  
This is a standard graph traversal problem applied on a 2D grid.

---

### 🔹 Problem Statement

You're given a 2D image represented as a matrix of integers. Each integer represents a pixel color.

You’re also given a starting pixel (`sr`, `sc`) and a `newColor`. Change the color of the starting pixel and **all pixels connected 4-directionally** (up/down/left/right) **with the same original color** to the new color.

---

### 🔹 Input and Output

**Input:**

- `image`: 2D matrix of `int`s
    
- `sr`, `sc`: row and column of the starting pixel
    
- `newColor`: the color to change to
    

**Output:**

- The updated image
    

---

### 🔹 Core Idea (Traversal Problem)

- You're doing a **graph traversal** (BFS or DFS) on a grid.
    
- You only **move to neighbors** (up/down/left/right) **if their color matches the original color**.
    
- Once visited, you change the color to avoid revisiting.
    

---

### 🔹 Why mark as visited **when enqueuing** in BFS?

- To **avoid adding the same node multiple times**.
    
- Marking early ensures **no redundant processing** and prevents TLE.
    
- ✅ BFS Rule of Thumb: **Mark visited when enqueueing** (NOT dequeueing).
    

---

### 🔹 ✅ BFS Solution (Safest, Correct Version)

```java
public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
    int originalColor = image[sr][sc];
    if (originalColor == newColor) return image;  // Nothing to change

    int rows = image.length;
    int cols = image[0].length;

    Queue<int[]> queue = new LinkedList<>();
    queue.add(new int[]{sr, sc});
    image[sr][sc] = newColor; // ✅ Mark as visited (paint) while enqueueing

    int[][] directions = {{0,1}, {0,-1}, {1,0}, {-1,0}}; // Right, Left, Down, Up

    while (!queue.isEmpty()) {
        int[] curr = queue.poll();
        int r = curr[0], c = curr[1];

        for (int[] dir : directions) {
            int nr = r + dir[0];
            int nc = c + dir[1];

            // Boundary and color match check
            if (nr >= 0 && nr < rows && nc >= 0 && nc < cols 
            && image[nr][nc] == originalColor) {
                queue.add(new int[]{nr, nc});
                image[nr][nc] = newColor; // ✅ Paint immediately to avoid revisits
            }
        }
    }

    return image;
}
```

---

### 🔹 DFS Version

```java
public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
    int originalColor = image[sr][sc];
    if (originalColor == newColor) return image;

    dfs(image, sr, sc, originalColor, newColor);
    return image;
}

private void dfs(int[][] image, int r, int c, int originalColor, int newColor) {
    // Boundary and color check
    if (r < 0 || r >= image.length || c < 0 || c >= image[0].length || image[r][c] != originalColor) {
        return;
    }

    image[r][c] = newColor; // ✅ Paint (mark as visited)

    dfs(image, r + 1, c, originalColor, newColor);
    dfs(image, r - 1, c, originalColor, newColor);
    dfs(image, r, c + 1, originalColor, newColor);
    dfs(image, r, c - 1, originalColor, newColor);
}
```

---

### 🔹 Time & Space Complexity

|Approach|Time Complexity|Space Complexity|
|---|---|---|
|BFS|O(N × M)|O(N × M) in worst case (queue)|
|DFS|O(N × M)|O(N × M) recursion stack (worst case flat image)|

> Where `N = rows`, `M = columns`. In the worst case, every pixel is visited.

---

### 🔹 Edge Case

```java
if (originalColor == newColor) return image;
```

- Prevents infinite loop or redundant traversal
    
- Since repainting already-colored nodes will keep going forever (DFS/BFS will not stop)
    

---

### 🔹 Flood Fill Variants to Practice

1. **Number of Islands** – LeetCode 200
    
2. **Max Area of Island** – LeetCode 695
    
3. **Surrounded Regions** – LeetCode 130
    
4. **Walls and Gates** – LeetCode 286
    
5. **Rotting Oranges** – LeetCode 994
    

---

### ✅ Summary

|Concept|BFS|DFS|
|---|---|---|
|When to mark visited|While adding to queue|While recursing|
|Space-efficient|✅ Better control|❌ Risk of StackOverflow|
|Safer for large graphs|✅|❌ Risky if recursion depth high|
|Common mistake|Mark after dequeue (wrong!)|Forget to stop condition|

---

Let me know if you’d like to add animation, visualization, or breakdown of each step with a sample matrix.