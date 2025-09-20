Here are the **full notes** for the **"Flatten Binary Tree to Linked List"** problem (Leetcode #114):

---

## ✅ Problem Statement

Given a binary tree, **flatten it to a linked list in-place**.

- The flattened tree should look like a **linked list using right pointers**.
    
- The order of the nodes should follow **preorder traversal** (root → left → right).
    
- Do **not use extra space** (i.e., must be done in-place).
    

---

### 🔍 Example

**Input Tree:**

```
      1
     / \
    2   5
   / \   \
  3   4   6
```

**Output Tree (flattened):**

```
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```

---

## 🔁 Intuition

We want to **flatten the tree into a right-skewed linked list** using **preorder traversal**:

- Visit root
    
- Flatten left subtree
    
- Flatten right subtree
    

### ✅ In-place Approach (Postorder / Reverse Preorder)

Use **reverse preorder** (right → left → root) to process nodes in reverse order and maintain a `prev` pointer.

---

## ✅ Java Code (Recursive, Optimal - O(n), O(h) space due to recursion)

```java
class Solution {
    private TreeNode prev = null; // Pointer to track previously visited node

    public void flatten(TreeNode root) {
        if (root == null) return;

        // Post-order reversed: right → left → root
        flatten(root.right);
        flatten(root.left);

        // Rewire the pointers
        root.right = prev;
        root.left = null;

        // Update prev
        prev = root;
    }
}
```

---

## ✅ Java Code (Iterative - Morris-like, O(n) time, O(1) space)

```java
class Solution {
    public void flatten(TreeNode root) {
        TreeNode curr = root;

        while (curr != null) {
            if (curr.left != null) {
                // Find the rightmost node of left subtree
                TreeNode pre = curr.left;
                while (pre.right != null) {
                    pre = pre.right;
                }

                // Connect right subtree to the rightmost node of left subtree
                pre.right = curr.right;

                // Move left subtree to the right
                curr.right = curr.left;
                curr.left = null;
            }

            // Move to next node (always to the right)
            curr = curr.right;
        }
    }
}
```

---

## 📘 Explanation of In-place Logic

For each node with a left child:

1. Find its **predecessor** (rightmost node of left subtree).
    
2. Connect the **original right subtree** to `predecessor.right`.
    
3. Move `node.left` to `node.right`.
    
4. Set `node.left = null`.
    

---

## ⏱ Time and Space Complexity

|Approach|Time|Space|
|---|---|---|
|Recursive|O(n)|O(h) (stack)|
|Iterative|O(n)|O(1)|

- `n` = number of nodes
    
- `h` = height of tree
    

---

## 🔄 Dry Run (Recursive)

Example:

```
      1
     / \
    2   5
```

Reverse Preorder:

- Start with 5 → set `5.right = null`, `prev = 5`
    
- Go to 2 → set `2.right = 5`, `prev = 2`
    
- Go to 1 → set `1.right = 2`, `prev = 1`
    

---

## 🧠 Key Ideas Recap

- **Reverse preorder** ensures right subtree is handled before left.
    
- Use `prev` to track the node to attach next.
    
- Set `left = null` at every node.
    
- **In-place** = no extra structures, just pointer rewiring.
    

---

## 📌 Interview Tips

- Clarify in-place requirement.
    
- Always check both left and right pointers during traversal.
    
- Be ready to explain **recursive vs iterative** tradeoffs.
    

---

Let me know if you’d like a visual dry-run or to practice variations like flattening **to doubly linked list** or using a **stack**.