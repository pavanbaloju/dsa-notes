### **Queues – Full Revision Index**

Queues are a **FIFO (First In, First Out)** data structure used in various problems related to ordering, scheduling, and processing sequential elements. This guide covers **all key patterns and problems** in queues.

---

## **1️⃣ Queue Basics**

- **What is a Queue?** – FIFO data structure
    
- **Operations** – `enqueue()`, `dequeue()`, `front()`, `rear()`, `isEmpty()`, `size()`
    
- **Implementation**
    
    - **Using an Array** - [[Queue implementation using array]]
        
    - **Using a Linked List** - [[Queue using LL]]
        
    - **Using Two Stacks** [[Queue using stacks]]
        

---

## **2️⃣ Queue Variants**

1. **Circular Queue** [[Queue implementation using array]]
    
    - Efficient queue implementation that wraps around to prevent unused space.
        
    - 🔹 **Problem:** Design Circular Queue 
        
2. **Deque (Double-Ended Queue)**
    
    - Allows insertion and deletion from both ends.
        
    - 🔹 **Problems:**
        
        - Sliding Window Maximum
            
        - [[Implement a deque]]
            
3. **Priority Queue (Min/Max Heap)**
    
    - Elements are processed based on priority, not FIFO order.
        
    - 🔹 **Problems:**
        
        - Kth Largest Element in a Stream
            
        - Merge K Sorted Lists
            

---

## **3️⃣ Monotonic Queue Pattern**

Maintains elements in increasing or decreasing order for **optimized sliding window processing**.  
🔹 **Problems:**

- [[Sliding window maximum]]
    
- Sum of Subarray Minimums

1. [[Monotonic Queues]]

---

## **4️⃣ BFS (Breadth-First Search) Pattern**

Queues are used to explore nodes level-by-level in graphs and trees.  
🔹 **Problems:**

- Binary Tree Level Order Traversal
    
- Shortest Path in Binary Matrix
    
- Rotting Oranges
    
- Word Ladder
    

---

## **5️⃣ Multi-Source BFS**

Processes multiple starting points at once using a queue.  
🔹 **Problems:**

- Rotten Oranges
    
- Walls and Gates
    

---

## **6️⃣ Queue-Based Scheduling & Simulation**

Used in **task scheduling, process execution, and round-robin processing**.  
🔹 **Problems:**

- Design Hit Counter
    
- Task Scheduler
    
- The Dining Philosophers
    

---

## **7️⃣ Stack using Queues**

🔹 **Problems:**

- Implement Stack using Queues (Two Approaches)
    

---

## **8️⃣ Queue using Stacks**

🔹 **Problems:**

- Implement Queue using Stacks
    

---

## **9️⃣ Josephus Problem (Circular Elimination)**

A famous problem involving circular queue processing.  
🔹 **Problem:** Josephus Problem

---

## **🔟 Top Interview Problems (Quick Revision)**

1. **Sliding Window Maximum (Deque)**
    
2. **Rotting Oranges (BFS)**
    
3. **Binary Tree Level Order Traversal (BFS)**
    
4. **Shortest Path in Binary Matrix (Multi-Source BFS)**
    
5. **Task Scheduler (Priority Queue)**
    
6. **Kth Largest Element in a Stream (Min Heap)**
    
7. **Merge K Sorted Lists (Min Heap)**
    
8. **Design Hit Counter (Queue Simulation)**
    
9. **Implement Stack using Queues**
    
10. **Implement Queue using Stacks**
    

---

This **revision guide** provides a **structured roadmap** to cover **all key patterns** in **queues**. Let me know if you need **detailed notes** on any specific section! 🚀