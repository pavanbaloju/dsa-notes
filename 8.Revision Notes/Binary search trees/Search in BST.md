Here are **full notes on “Search in a Binary Search Tree (BST)”** – covering concept, Java implementations (recursive & iterative), edge cases, time/space complexity, and related patterns.

---

## ✅ Problem Statement:

Given the root of a Binary Search Tree and a value `val`, return the node in the BST where the node's value equals `val`. If the value does not exist in the BST, return `null`.

---

## ✅ BST Property Recap

In a BST:

- Left subtree contains values **less than** the node.
    
- Right subtree contains values **greater than** the node.
    
- This helps in **binary search**, which gives better performance than linear traversal.
    

---

## ✅ Java Code – Recursive Approach

```java
public class Solution {
    public TreeNode searchBST(TreeNode root, int val) {
        if (root == null || root.val == val) {
            return root;
        }

        if (val < root.val) {
            return searchBST(root.left, val);
        } else {
            return searchBST(root.right, val);
        }
    }
}
```

---

## ✅ Java Code – Iterative Approach (no recursion stack)

```java
public class Solution {
    public TreeNode searchBST(TreeNode root, int val) {
        while (root != null) {
            if (val == root.val) {
                return root;
            } else if (val < root.val) {
                root = root.left;
            } else {
                root = root.right;
            }
        }
        return null;
    }
}
```

---

## ✅ Time and Space Complexity

|Aspect|Recursive|Iterative|
|---|---|---|
|Time|O(h)|O(h)|
|Space|O(h) (call stack)|O(1)|

Where **h** = height of the tree.

- Best case: O(log N) in a balanced BST
    
- Worst case: O(N) in a skewed BST (like a linked list)
    

---

## ✅ Edge Cases

- `root == null`: Return `null`
    
- Value not present in tree: Return `null`
    
- Value present at root: Return `root` node
    
- Value in deepest leaf: Still reachable via BST property
    

---

## 🔁 Related Problems / Patterns

|Problem|Pattern|
|---|---|
|Insert into BST|BST Traversal|
|Delete from BST|BST Recursion|
|Validate BST|BST Range Check|
|Lowest Common Ancestor in BST|BST + Path logic|
|Closest Value in BST|BST + Binary Search|

---

## ✅ Summary

- **Recursive** is easier to write and read.
    
- **Iterative** is more memory-efficient (no call stack).
    
- You leverage the **BST property** to discard half the tree at each step – that's the key.
    

---

Would you like the “Insert in BST” notes next (often asked together)?