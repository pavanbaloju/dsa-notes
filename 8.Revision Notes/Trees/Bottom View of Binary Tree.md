### 🌳 Bottom View of a Binary Tree – Full Notes

---

### ✅ **Problem Statement**

Given the root of a binary tree, return the **bottom view** of the tree.  
**Bottom view** refers to the **last visible node** (i.e., the lowest one) at each vertical level when the tree is viewed from the bottom.

---

### 📌 **Example**

For the tree:

```
         1
       /   \
      2     3
       \   / \
        4 5   6
```

**Bottom view**: `2 4 5 3 6`  
(From leftmost vertical to rightmost: node with lowest vertical level is picked for each horizontal distance)

---

### 🧠 **Concepts Involved**

1. **Horizontal Distance (HD)**:
    
    - Root node: HD = 0
        
    - Left child: HD = parent HD - 1
        
    - Right child: HD = parent HD + 1
        
2. Use **BFS (Level Order Traversal)** to visit nodes level by level:
    
    - Update the **map at every HD** (unlike Top View where you set only if not visited).
        
    - The **last node** encountered at each HD will be in the bottom view.
        

---

### ✅ **Approach (BFS + HashMap)**

1. Use a **queue** to perform BFS. Each item in queue stores `(node, horizontal distance)`.
    
2. Use a **`TreeMap<Integer, Integer>`** to track the node values at each HD.
    
    - `TreeMap` automatically keeps HDs sorted.
        
3. In BFS traversal:
    
    - **Always update** the map with the current node's value for its HD.
        

---

### ✅ **Java Code**

```java
class Solution {
    public List<Integer> bottomView(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;

        Map<Integer, Integer> hdMap = new TreeMap<>(); // HD -> node value
        Queue<Pair<TreeNode, Integer>> queue = new LinkedList<>();

        queue.offer(new Pair<>(root, 0));

        while (!queue.isEmpty()) {
            Pair<TreeNode, Integer> current = queue.poll();
            TreeNode node = current.getKey();
            int hd = current.getValue();

            // Always overwrite with the latest node at that horizontal distance
            hdMap.put(hd, node.val);

            if (node.left != null) {
                queue.offer(new Pair<>(node.left, hd - 1));
            }
            if (node.right != null) {
                queue.offer(new Pair<>(node.right, hd + 1));
            }
        }

        for (int val : hdMap.values()) {
            result.add(val);
        }

        return result;
    }
}
```

---

### 🧾 **Time and Space Complexity**

- **Time**: `O(N log HD)` due to TreeMap operations
    
- **Space**: `O(N)` for map and queue
    

---

### ✅ **Key Differences from Top View**

|Aspect|Top View|Bottom View|
|---|---|---|
|When to store|First node at each HD|Last node at each HD|
|Map update rule|Only if not already present|Always update (overwrite)|
|Use case|View from top|View from bottom|

---

### 🧠 **Follow-up / Related Problems**

- Top View of Binary Tree
    
- Vertical Order Traversal
    
- Diagonal Traversal
    
- Left/Right View
    

Would you like me to cover **Vertical Order Traversal** or **Left/Right View** next?