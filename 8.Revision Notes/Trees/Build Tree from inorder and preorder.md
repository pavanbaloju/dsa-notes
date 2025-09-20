Here are full detailed notes for constructing a **Binary Tree** from **Inorder and Preorder Traversal**:

---

### ✅ **Problem Statement**

Given two arrays:

- `preorder[]` – preorder traversal of a binary tree
    
- `inorder[]` – inorder traversal of the same binary tree
    

Construct the original binary tree and return its root.

---

### 🧠 **Key Insight**

- **Preorder Traversal**: `[Root, Left Subtree, Right Subtree]`
    
- **Inorder Traversal**: `[Left Subtree, Root, Right Subtree]`
    

The first element of preorder is always the **root**. Use that to find the root's index in inorder traversal to separate left and right subtrees.

---

### 🪜 **Steps to Solve**

1. Start with the first element in preorder → this is the root.
    
2. Find the index of this root in the inorder array.
    
3. All elements left to the index in inorder → left subtree.
    
4. All elements right to the index in inorder → right subtree.
    
5. Recursively do the same for left and right subtree.
    
6. Use a **hashmap** for `inorder` indices to avoid O(n) lookups.
    

---

### 📦 **Java Code**

```java
class Solution {
    int preorderIndex = 0;
    Map<Integer, Integer> inorderMap = new HashMap<>();

    public TreeNode buildTree(int[] preorder, int[] inorder) {
        // Store value -> index for fast lookup in inorder array
        for (int i = 0; i < inorder.length; i++) {
            inorderMap.put(inorder[i], i);
        }
        return build(preorder, 0, inorder.length - 1);
    }

    private TreeNode build(int[] preorder, int inStart, int inEnd) {
        // Base case: no elements to build subtree
        if (inStart > inEnd) return null;

        // Get root from current preorder index
        int rootVal = preorder[preorderIndex++];
        TreeNode root = new TreeNode(rootVal);

        // Find root in inorder array
        int inIndex = inorderMap.get(rootVal);

        // Recursively build left and right subtrees
        root.left = build(preorder, inStart, inIndex - 1);
        root.right = build(preorder, inIndex + 1, inEnd);

        return root;
    }
}
```

---

### 🧮 **Time and Space Complexity**

- **Time**: `O(n)`
    
    - Each node is visited once
        
    - Lookup in `HashMap` is O(1)
        
- **Space**: `O(n)`
    
    - HashMap + recursion stack (O(height), worst O(n))
        

---

### 🔍 **Example**

#### Input:

```java
preorder = [3,9,20,15,7]
inorder =  [9,3,15,20,7]
```

#### Output:

```
      3
     / \
    9  20
       / \
      15  7
```

---

### 🧠 **Concept Summary**

|Traversal|Order|
|---|---|
|Preorder|Root → Left → Right|
|Inorder|Left → Root → Right|

We keep moving through the **preorder array** to pick roots, and we use the **inorder array** to decide how to split into left and right subtrees.

---

Let me know if you'd like the same explanation for **Inorder + Postorder** or **Inorder + Level Order**.