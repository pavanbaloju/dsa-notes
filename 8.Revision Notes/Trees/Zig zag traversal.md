Here are **full notes on Zigzag Level Order Traversal** of a binary tree – also called **spiral traversal**.

---

## 🌳 Problem: Zigzag Level Order Traversal

(LeetCode 103 - [Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/))

---

## 🧾 Problem Statement

Given the root of a binary tree, return the **zigzag level order traversal** of its nodes' values.  
(i.e., left to right, then right to left for the next level and alternate between.)

---

## 🧠 Intuition

It is a **level order traversal** (like BFS), but alternates the **direction** of reading nodes:

- Level 0 → left to right
    
- Level 1 → right to left
    
- Level 2 → left to right
    
- And so on...
    

---

## ✅ Input and Output

### Input:

A binary tree root node.

### Output:

A `List<List<Integer>>` where each list contains the node values of a level in zigzag order.

---

## ✅ Approach: BFS with Direction Toggle

### 💡 Idea:

- Use a **Queue** to do normal level order traversal.
    
- Maintain a boolean flag `leftToRight` to alternate the order.
    
- For each level:
    
    - Create a temporary list of that level's nodes.
        
    - If `leftToRight`, add nodes to the end of the list.
        
    - If not, add nodes to the **front** of the list (reverse direction).
        
- Flip the `leftToRight` flag after each level.
    

---

### ✅ Java Code:

```java
class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int x) { val = x; }
}

public class ZigzagTraversal {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) return result;

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        boolean leftToRight = true;

        while (!queue.isEmpty()) {
            int size = queue.size();
            LinkedList<Integer> level = new LinkedList<>();

            for (int i = 0; i < size; i++) {
                TreeNode current = queue.poll();

                // Add node value in the appropriate direction
                if (leftToRight) {
                    level.addLast(current.val);
                } else {
                    level.addFirst(current.val);
                }

                // Add children for next level
                if (current.left != null) queue.offer(current.left);
                if (current.right != null) queue.offer(current.right);
            }

            result.add(level);
            leftToRight = !leftToRight; // Flip direction
        }

        return result;
    }
}
```

---

## 🔁 Dry Run Example

Given this tree:

```
        1
       / \
      2   3
     / \   \
    4   5   6
```

Zigzag traversal is:

```
[
 [1],        // left to right
 [3, 2],     // right to left
 [4, 5, 6]   // left to right
]
```

---

## 📊 Time and Space Complexity

|Metric|Complexity|
|---|---|
|Time|`O(n)` – each node is visited once|
|Space|`O(n)` – for queue and result list|

---

## 🧠 Alternate Approach: Two Stacks (Optional)

If you don’t want to reverse lists or addFirst/addLast, you can use two stacks:

- `currentLevel` stack and `nextLevel` stack
    
- Use one for left-to-right, the other for right-to-left.
    

Let me know if you want this version too.

---

## 🧪 Test Cases

### ✅ Test Case 1:

```java
Input:
        1
       / \
      2   3
Output: [[1], [3, 2]]
```

### ✅ Test Case 2:

```java
Input:
        1
Output: [[1]]
```

### ✅ Test Case 3:

```java
Input: null
Output: []
```

---

## ✅ Summary

- Zigzag is just level order + direction alternation.
    
- Use a `Queue` and a `LinkedList<Integer>` to efficiently handle direction changes.
    
- Flip `leftToRight` after each level.
    

---

Would you like the **two stacks approach** or a **visual walkthrough** next?