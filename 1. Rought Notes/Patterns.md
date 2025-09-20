## **Comprehensive List of DSA Patterns for Problem-Solving**

Below is a categorized list of **DSA problem patterns** that commonly appear in **coding interviews** and **competitive programming**.

---

### **1. Array and Two-Pointer Patterns**

|**Pattern**|**Description**|**Example Problems**|
|---|---|---|
|**Two Pointers**|Uses two pointers to traverse/search an array.|Two Sum (Sorted), Three Sum, Container with Most Water|
|**Sliding Window**|Expands and contracts a window dynamically to optimize subarrays.|Longest Substring Without Repeating Characters, Smallest Subarray with Sum ≥ K|
|**Prefix Sum**|Precomputes cumulative sums to answer range sum queries in O(1).|Subarray Sum Equals K, Range Sum Query|
|**Difference Array**|Applies range updates efficiently in O(1).|Range Increment Queries|
|**Kadane’s Algorithm**|Finds the maximum sum of a contiguous subarray in O(n).|Maximum Subarray Sum|
|**Dutch National Flag (Three-Way Partitioning)**|Sorts an array with three distinct elements in O(n).|Sort Colors (0s, 1s, 2s)|
|**Cyclic Sort**|Sorts numbers when elements are in a fixed range (1 to N).|Find Missing Number, First Missing Positive|

---

### **2. Linked List Patterns**

|**Pattern**|**Description**|**Example Problems**|
|---|---|---|
|**Slow and Fast Pointers**|Uses two pointers moving at different speeds.|Detect Cycle in Linked List, Find Middle of Linked List|
|**Reversal of a Linked List**|Reverses a portion or entire linked list.|Reverse Linked List, Reverse Nodes in k-Group|
|**Merging Two Sorted Lists**|Combines two sorted linked lists efficiently.|Merge Two Sorted Lists|
|**Linked List Cycle Detection**|Detects cycles using Floyd’s Tortoise and Hare Algorithm.|Detect Cycle in Linked List|
|**Finding Intersection in Two Linked Lists**|Determines where two linked lists merge.|Intersection of Two Linked Lists|

---

### **3. Stack and Queue Patterns**

|**Pattern**|**Description**|**Example Problems**|
|---|---|---|
|**Monotonic Stack**|Maintains a stack in increasing/decreasing order.|Next Greater Element, Largest Rectangle in Histogram|
|**Monotonic Queue**|Uses deque for efficient range maximum/minimum queries.|Sliding Window Maximum|
|**Parentheses Matching**|Uses a stack to validate balanced parentheses.|Valid Parentheses, Longest Valid Parentheses|
|**Stack-Based Backtracking**|Uses stack for iterative DFS or undo operations.|Basic Calculator, Remove K Digits|

---

### **4. Sorting and Searching Patterns**

|**Pattern**|**Description**|**Example Problems**|
|---|---|---|
|**Binary Search**|Efficiently searches sorted data in O(log n).|Find Minimum in Rotated Sorted Array, Search in a Sorted Matrix|
|**Binary Search on Answer**|Uses binary search in problems where the answer space is sorted.|Koko Eating Bananas, Capacity to Ship Packages|
|**Two Heaps (Min-Heap & Max-Heap)**|Uses two heaps to track median efficiently.|Find Median from Data Stream|
|**Bucket Sort / Counting Sort**|Used when elements are within a known range.|Sort an Array, Top K Frequent Elements|
|**Merge Intervals**|Merges overlapping intervals.|Merge Intervals, Meeting Rooms II|

---

### **5. Graph Patterns**

|**Pattern**|**Description**|**Example Problems**|
|---|---|---|
|**Breadth-First Search (BFS)**|Explores neighbors level by level.|Shortest Path in Unweighted Graph, Number of Islands|
|**Depth-First Search (DFS)**|Recursively explores deeper nodes first.|Connected Components in Graph, Detect Cycle in Graph|
|**Topological Sorting (Kahn’s Algorithm, DFS-Based)**|Finds a valid order in a Directed Acyclic Graph (DAG).|Course Schedule, Task Scheduling|
|**Dijkstra’s Algorithm**|Finds shortest path in a weighted graph.|Shortest Path in Graph|
|**Bellman-Ford Algorithm**|Finds shortest paths in graphs with negative weights.|Single Source Shortest Path|
|**Floyd-Warshall Algorithm**|Finds all-pairs shortest paths.|Network Delay Time|
|**Union-Find (Disjoint Set)**|Detects connected components efficiently.|Graph Connectivity, Kruskal’s Algorithm|

---

### **6. Tree and Binary Search Tree (BST) Patterns**

|**Pattern**|**Description**|**Example Problems**|
|---|---|---|
|**DFS Traversals (Preorder, Inorder, Postorder)**|Recursive or iterative traversal of trees.|Binary Tree Inorder Traversal|
|**BFS Traversal (Level Order)**|Traverses tree level by level using a queue.|Binary Tree Level Order Traversal|
|**Lowest Common Ancestor (LCA)**|Finds LCA of two nodes in a BST or tree.|LCA in Binary Tree|
|**BST Insertion, Deletion, Search**|Performs standard BST operations efficiently.|Insert into BST, Delete Node in BST|

---

### **7. Dynamic Programming (DP) Patterns**

|**Pattern**|**Description**|**Example Problems**|
|---|---|---|
|**Knapsack DP**|0/1 Knapsack, Partition Equal Subset Sum.|Subset Sum, Coin Change|
|**Fibonacci-Style DP**|Optimizes recursive problems with overlapping subproblems.|Climbing Stairs, House Robber|
|**Matrix DP**|Used for grid-based DP problems.|Unique Paths, Minimum Path Sum|
|**Substring DP**|Finds longest common substrings or subsequences.|Longest Common Subsequence, Longest Palindromic Substring|
|**Bitmask DP**|Solves problems involving subsets efficiently.|Traveling Salesman Problem|

---

### **8. Greedy Patterns**

|**Pattern**|**Description**|**Example Problems**|
|---|---|---|
|**Interval Scheduling**|Selects the maximum number of non-overlapping intervals.|Activity Selection Problem|
|**Huffman Coding (Greedy Tree)**|Compresses data using a frequency-based tree.|Huffman Encoding|
|**Greedy Graph Algorithms**|Kruskal’s and Prim’s Algorithms for MST.|Minimum Spanning Tree|

---

### **9. Bit Manipulation Patterns**

|**Pattern**|**Description**|**Example Problems**|
|---|---|---|
|**Bitwise Operations**|Uses AND, OR, XOR, Shift operations.|Single Number, Subset Generation|
|**Bitmasking for Subsets**|Represents subsets using bits.|Traveling Salesman Problem|
|**Gray Code Generation**|Generates sequences of binary numbers differing by one bit.|Gray Code Problem|

---

### **10. Mathematical and Number Theory Patterns**

|**Pattern**|**Description**|**Example Problems**|
|---|---|---|
|**Modular Arithmetic**|Used to compute large exponentiation.|Modular Exponentiation|
|**GCD and LCM**|Finds greatest common divisor and least common multiple.|GCD of Array, Euclidean Algorithm|
|**Sieve of Eratosthenes**|Finds all prime numbers up to N efficiently.|Count Primes|

---

### **Next Steps**

You’ve already covered: ✔ Two Pointers  
✔ Sliding Window  
✔ Prefix Sum  
✔ Slow and Fast Pointer

Would you like to continue with **Monotonic Stack/Queue, Union-Find (Disjoint Set), Trie (Prefix Tree), or Dynamic Programming next?**