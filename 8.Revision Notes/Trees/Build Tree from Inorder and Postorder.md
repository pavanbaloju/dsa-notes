Great! Here's the **full version of "Construct Binary Tree from Inorder and Postorder Traversal"** using **class variables** for cleaner recursion:

---

## ✅ Problem: Construct Binary Tree from Inorder and Postorder

Given:

- `inorder[]`: Left → Root → Right
    
- `postorder[]`: Left → Right → Root
    

Goal:  
Construct the binary tree and return the root.

---

## 🔍 Key Observations

1. The **last element** in `postorder` is always the **root**.
    
2. Once we find the root in `inorder`, we can:
    
    - Divide the array into **left** and **right** subtrees.
        
3. Process **postorder from right to left**, building the tree from bottom up.
    

---

## ✅ Java Code (With Class Variables)

```java
class Solution {
    private int postIndex;
    private Map<Integer, Integer> inorderMap;

    public TreeNode buildTree(int[] inorder, int[] postorder) {
        // Initialize postIndex to last index of postorder
        postIndex = postorder.length - 1;

        // Build a value -> index map from inorder
        inorderMap = new HashMap<>();
        for (int i = 0; i < inorder.length; i++) {
            inorderMap.put(inorder[i], i);
        }

        // Recursively build the tree
        return build(postorder, 0, inorder.length - 1);
    }

    private TreeNode build(int[] postorder, int inStart, int inEnd) {
        // Base case: no subtree to process
        if (inStart > inEnd || postIndex < 0) {
            return null;
        }

        // Get the current root value from postorder
        int rootVal = postorder[postIndex--];
        TreeNode root = new TreeNode(rootVal);

        // Get root index in inorder
        int inIndex = inorderMap.get(rootVal);

        // Build right subtree first (important!)
        root.right = build(postorder, inIndex + 1, inEnd);
        root.left = build(postorder, inStart, inIndex - 1);

        return root;
    }
}
```

---

## 🧠 Why Build Right Before Left?

In **postorder**, the traversal is:  
`Left → Right → Root`

But since we are going **backward from end to start**, we encounter:

`Root → Right → Left`

So when building recursively, we must **build the right subtree first**, then the left.

---

## ⏱ Time and Space Complexity

|Aspect|Complexity|
|---|---|
|**Time**|O(n)|
|**Space** (Map)|O(n)|
|**Space** (Stack)|O(h) worst case O(n)|

- `n` = number of nodes
    
- `h` = height of tree
    

---

## 📘 Example

Given:

```java
inorder   = [9, 3, 15, 20, 7]
postorder = [9, 15, 7, 20, 3]
```

Steps:

- postorder[4] = 3 → root
    
- 3 at index 1 in inorder
    
    - left = [9], right = [15, 20, 7]
        
- postorder[3] = 20 → right root
    
- continue recursively
    

---

## ✅ Summary

|Step|Description|
|---|---|
|postorder[last]|Root of tree|
|HashMap|Stores inorder value:index|
|Build right before left|Due to postorder reverse traversal|
|Class variables used|`postIndex`, `inorderMap`|

---

Let me know if you’d like a **preorder + inorder** version or a **dry-run visual** next.