Here's the **Morris Inorder Traversal** Java code with **detailed comments on every line**, explaining exactly what's happening and why:

---

### ✅ Morris Inorder Traversal – Fully Commented Java Code

```java
public List<Integer> morrisInorder(TreeNode root) {
    List<Integer> result = new ArrayList<>();         // To store the final inorder traversal
    TreeNode current = root;                          // Start traversal from root

    while (current != null) {                         // Continue until all nodes are processed
        if (current.left == null) {                   // Case 1: No left subtree
            result.add(current.val);                  // Visit current node
            current = current.right;                  // Move to right child
        } else {
            // Case 2: Left subtree exists — need to find predecessor
            TreeNode predecessor = current.left;      // Go to left child
            while (predecessor.right != null &&       // Find rightmost node in left subtree
                   predecessor.right != current) {    // Also make sure we don’t revisit the thread
                predecessor = predecessor.right;
            }

            if (predecessor.right == null) {
                // Step 1 of threading: create a temporary link back to current
                predecessor.right = current;          // Thread rightmost node's right to current
                current = current.left;               // Move to left subtree
            } else {
                // Step 2 of threading: thread already exists, which means left is done
                predecessor.right = null;             // Remove the thread (restore tree)
                result.add(current.val);              // Visit current node
                current = current.right;              // Move to right subtree
            }
        }
    }

    return result;                                     // Final inorder traversal result
}
```

---

### 🔁 Summary of Key Ideas:

- **No Stack, No Recursion**: Uses O(1) space by temporarily changing tree pointers.
    
- **Threading**: Connects predecessor's `.right` to current so we can come back after left subtree.
    
- **Restoration**: Always restore the tree before moving right.
    

---

Would you like the same **commented code for Preorder Morris**, or a **diagram-based step-by-step dry run** to visualize how the threading works?