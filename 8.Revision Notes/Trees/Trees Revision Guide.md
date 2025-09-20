Here’s a **comprehensive and structured list of all major tree patterns** you should know for interviews, especially focused on **binary trees** and **binary search trees**, with the most relevant problems and use cases:

---

## 🌳 **TREE PATTERNS FOR INTERVIEWS**

---

### 1️⃣ **Traversal Patterns**

#### 🔁 **Recursive Traversals**

- Inorder (Left, Root, Right) → Used in BSTs
    
- Preorder (Root, Left, Right) → Used to clone trees, reconstruct trees
    
- Postorder (Left, Right, Root) → Used to delete or process children first
    

#### 🔄 **Iterative Traversals (Using Stack)**

- Inorder / Preorder / Postorder without recursion
    

#### 📶 **Level Order (BFS Traversal)**

- Classic BFS using Queue
    
- With level distinction or without
    
- Zigzag Level Order (Leetcode 103)
    

---

### 2️⃣ **Depth-First Search (DFS)**

- Used in problems where recursion or stack is needed to explore all paths
    
- Preorder DFS: Good for backtracking-type problems
    
- Postorder DFS: Used for bottom-up aggregation (like subtree calculations)
    

---

### 3️⃣ **Tree Construction Patterns**

#### 🔨 **From Traversals**

- Inorder + Preorder → Rebuild binary tree
    
- Inorder + Postorder → Rebuild binary tree
    
- Preorder with null markers → Serialize/deserialize trees
    

---

### 4️⃣ **Binary Search Tree (BST) Patterns**

#### 🔎 **Properties of BST**

- Left < Root < Right
    
- Sorted Inorder Traversal
    

#### 🧠 **Problems**

- Validate BST
    
- Find Kth smallest/largest
    
- Convert BST to DLL
    
- Lowest Common Ancestor in BST
    
- Range sum in BST
    
- Delete Node from BST
    

---

### 5️⃣ **Diameter / Height / Depth / Balance**

#### 🔢 **Key Problems**

- Height of Tree (DFS)
    
- Depth (Min/Max) → BFS or DFS
    
- Balanced Tree Check
    
- Diameter of Binary Tree (Max path between any two nodes)
    

---

### 6️⃣ **Lowest Common Ancestor (LCA)**

- In Binary Tree: Check both subtrees recursively
    
- In BST: Use BST properties for efficient solution
    

---

### 7️⃣ **Path-Based Problems**

#### 🛣️ **Common Types**

- Path Sum (check if root-to-leaf has a given sum)
    
- All Paths from Root to Leaf
    
- Max Path Sum (any path, not just root-leaf)
    
- Count Paths with Sum (prefix sum trick in trees)
    

---

### 8️⃣ **Views of a Tree**

#### 👁️ **Different Views**

- Left View
    
- Right View
    
- Top View
    
- Bottom View
    
- Vertical Order Traversal
    
- Diagonal View
    

---

### 9️⃣ **Serialization / Deserialization**

- Encode a tree as string
    
- Decode string to rebuild tree
    
- Use Preorder or Level Order + null markers
    

---

### 🔟 **Morris Traversal (Threaded Binary Trees)**

- Inorder Traversal using O(1) space (no recursion or stack)
    

---

### 1️⃣1️⃣ **Tree to DLL / Flattening Trees**

- Convert Binary Tree to Doubly Linked List (inorder-like)
    
- Flatten Binary Tree to Linked List (Preorder-style)
    

---

### 1️⃣2️⃣ **Subtree / Identical Tree Problems**

- Is Subtree of Another
    
- Are Trees Identical
    

---

### 1️⃣3️⃣ **Tree to Graph-like Problems**

- Burning Tree
    
- Amount of Time to Inform All Employees
    
- Minimum Time to Burn a Tree (Node → Parent relationship + BFS)
    

---

### 1️⃣4️⃣ **Backtracking on Trees**

- N-ary Trees
    
- All possible binary trees with `n` nodes (Full Binary Trees)
    
- Construct Binary Trees from given constraints
    

---

### 1️⃣5️⃣ **Advanced Patterns**

#### 🔁 **Recursive Aggregation**

- Bottom-up DP (e.g., House Robber III)
    
- Count Good Nodes
    
- Count Univalue Subtrees
    

#### 📊 **Binary Lifting / LCA with Preprocessing**

- Used in advanced interview problems or CP
    

---

## ✅ Want to go topic by topic with problem sets?

Let me know and I’ll give you a **pattern-wise Leetcode list** for practice.