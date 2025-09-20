### 🌳 Top View of a Binary Tree – Full Notes

---

### ✅ **Problem Statement**

Given the root of a binary tree, return the **top view** of the tree.  
**Top view** means: when the tree is viewed from the **top**, what nodes are visible (i.e., the first node at each vertical level from top to bottom).

---

### 📌 **Example**

For this tree:

```
        1
      /   \
     2     3
      \   / \
       4 5   6
```

**Top view**: `2 1 3 6`  
(From leftmost vertical level to rightmost: 2 (leftmost), 1 (center), 3 and 6 (rightmost))

---

### 🧠 **Concepts Involved**

1. **Horizontal Distance (HD)**:
    
    - Root has HD = 0
        
    - Left child has HD = parent HD - 1
        
    - Right child has HD = parent HD + 1
        
2. **Top view** needs:
    
    - First node encountered at every HD (vertical level)
        
3. Use **BFS (Level Order Traversal)** to ensure we see the topmost node first for each HD.
    

---

### ✅ **Approach (BFS + HashMap)**

1. Use a `Queue` to do level order traversal. Each entry will store `(node, horizontal distance)`.
    
2. Use a `TreeMap` or `HashMap<Integer, Integer>` to record the first node at each HD.
    
    - `TreeMap` gives sorted HDs (left to right).
        
3. For each node:
    
    - If the HD is not yet in the map, record it.
        
    - Enqueue left and right children with updated HDs.
        

---

### ✅ **Java Code**

```java
class Solution {
    public List<Integer> topView(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;

        // Queue for level order traversal: stores (node, horizontal distance)
        Queue<Pair<TreeNode, Integer>> queue = new LinkedList<>();
        Map<Integer, Integer> topViewMap = new TreeMap<>(); // TreeMap keeps keys sorted

        queue.offer(new Pair<>(root, 0));

        while (!queue.isEmpty()) {
            Pair<TreeNode, Integer> current = queue.poll();
            TreeNode node = current.getKey();
            int hd = current.getValue();

            // Store the first node at every horizontal distance
            if (!topViewMap.containsKey(hd)) {
                topViewMap.put(hd, node.val);
            }

            if (node.left != null) {
                queue.offer(new Pair<>(node.left, hd - 1));
            }
            if (node.right != null) {
                queue.offer(new Pair<>(node.right, hd + 1));
            }
        }

        // Collect results from leftmost to rightmost HD
        for (int val : topViewMap.values()) {
            result.add(val);
        }

        return result;
    }
}
```

---

### 🧾 **Time and Space Complexity**

- **Time**: `O(N log HD)` (due to TreeMap operations)
    
- **Space**: `O(N)` for map and queue
    

---

### ✅ **Use Cases**

- Visual representation of a tree from the top
    
- Interview problem involving BFS + Hashing + Tree traversal
    
- Related problems:
    
    - Bottom view of binary tree
        
    - Vertical order traversal
        

---

Would you like **Bottom View** or **Vertical Order Traversal** notes next?