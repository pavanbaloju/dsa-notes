### **Linked List Variations – Detailed Breakdown**

---

## **1️⃣ Singly Linked List**

- Each node has **one pointer** pointing to the next node.
- **Operations:** Insert, delete, reverse, detect cycle.
- **Use Cases:** Stacks, queues, adjacency lists in graphs.

🔹 **Example Problems:**

- **Implement Singly Linked List**
- **Leetcode 206 – Reverse Linked List**
- **Leetcode 876 – Find Middle of Linked List**

1. [[Singly Linked List Implementation]]
2. 

---

## **2️⃣ Doubly Linked List**

- Each node has **two pointers**:
    - `next` (points to next node)
    - `prev` (points to previous node)
- **Operations:** Insert at head/tail, delete node, reverse traversal.
- **Use Cases:** LRU Cache, Navigable History (Browser Back/Forward).

🔹 **Example Problems:**

- **Leetcode 146 – LRU Cache (Doubly Linked List + HashMap)**
- **Implement a Doubly Linked List**

1.  [[Doubly linked list implementation]]

---

## **3️⃣ Circular Linked List**

- Last node points **back to the first node** instead of `null`.
- **Operations:** Detect cycle, remove cycle, fast & slow pointers.
- **Use Cases:** Round-robin scheduling, buffering.

🔹 **Example Problems:**

- **Leetcode 141 – Detect Cycle in a Linked List**
- **Leetcode 142 – Find Start of Cycle (Cycle II)**
- **Leetcode 61 – Rotate Linked List**

---

## **4️⃣ Merging & Sorting Linked Lists**

- **Merge two sorted linked lists efficiently.**
- **Sort a linked list using Merge Sort (O(n log n))**.

🔹 **Example Problems:**

- **Leetcode 21 – Merge Two Sorted Lists**
- **Leetcode 23 – Merge `k` Sorted Lists**
- **Leetcode 148 – Sort Linked List**

 1. [[Merge two sorted lists]]

---

## **5️⃣ Cycle Detection & Removal**

- **Detect a cycle using Floyd’s Cycle Detection Algorithm (Slow & Fast Pointers).**
- **Find the starting node of the cycle.**
- **Remove a cycle from a linked list.**

🔹 **Example Problems:**

- **Leetcode 141 – Detect Cycle in a Linked List**
- **Leetcode 142 – Find Cycle Start in Linked List**
- **Leetcode 287 – Find the Duplicate Number (Similar Approach)**

1. [[Detect cycle in linked list]]
2. [[Find cycle start in linked list]]

---

## **6️⃣ Reversal & Rotation**

- **Reverse a full linked list (Iterative & Recursive).**
- **Reverse a sublist (Between `left` and `right`).**
- **Rotate linked list by `k` places.**

🔹 **Example Problems:**

- **Leetcode 206 – Reverse Linked List**
- **Leetcode 92 – Reverse Linked List II**
- **Leetcode 61 – Rotate Linked List**

1. [[Reverse a linked list]]
2. [[Reverse a linked list ii]]
3. [[Rotate a linked list]]

---

## **7️⃣ Fast & Slow Pointer Technique**

- **Find the middle of a linked list.**
- **Detect cycle in a linked list.**
- **Find the nth node from the end.**

🔹 **Example Problems:**

- **Leetcode 876 – Find Middle of Linked List**
- **Leetcode 141 – Detect Cycle in a Linked List**
- **Leetcode 19 – Remove Nth Node From End**

1. [[Remove nth node from end]]
2. [[Intersection of Y linked lists]]

---

## **8️⃣ Linked List Intersection & Merging**

- **Find the intersection point of two linked lists.**
- **Merge two sorted linked lists.**
- **Merge `k` sorted linked lists using a min heap.**

🔹 **Example Problems:**

- **Leetcode 160 – Intersection of Two Linked Lists**
- **Leetcode 21 – Merge Two Sorted Lists**
- **Leetcode 23 – Merge `k` Sorted Lists**

1. [[Intersection of Y linked lists]]
2. [[Merge two sorted lists]]

---

## **9️⃣ Linked List Palindrome & Reordering**

- **Check if a linked list is a palindrome.**
- **Reorder a linked list (Rearrange elements to `L0 → Ln → L1 → Ln-1` format).**

🔹 **Example Problems:**

- **Leetcode 234 – Palindrome Linked List**
- **Leetcode 143 – Reorder Linked List**

---

## **🔟 Special Linked List Variants**

- **Flatten a multilevel linked list (A linked list where nodes can have child pointers).**
- **Copy a linked list with random pointers.**

🔹 **Example Problems:**

- **Leetcode 430 – Flatten a Multilevel Doubly Linked List**
- **Leetcode 138 – Copy List with Random Pointer**

1. [[Copy list with random pointer]]

---

## **Final Takeaways**

- **Two-Pointer Techniques** are widely used for cycle detection, intersection, and palindrome checks.
- **Merge & Sort Operations** play a crucial role in Linked List manipulation.
- **Fast & Slow Pointers** are key to solving middle element, cycle detection, and nth node problems.
- **Reversal and Rotation** problems frequently appear in technical interviews.

Would you like **detailed explanations of any specific problem?** 🚀