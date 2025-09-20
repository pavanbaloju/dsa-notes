Here's a complete DSA breakdown of the classic implementation problem:

---

# ✅ Problem: **Implement Stack using Queue**

(Leetcode 225 – [Implement Stack using Queues](https://leetcode.com/problems/implement-stack-using-queues/))

---

## 🔹 Problem Statement

> Implement a **Last-In-First-Out (LIFO)** stack using **only queue operations**:

- `push(x)`, `pop()`, `top()`, `empty()`
    

Only use:

- `offer()` / `add()` (enqueue)
    
- `poll()` / `remove()` (dequeue)
    
- `peek()`
    
- `isEmpty()`
    

---

## 🔁 Pattern

- **Queue Simulation**
    
- Choose between:
    
    - **Costly `push`** (make the newest element come to front)
        
    - **Costly `pop`** (remove all elements until last inserted)
        

---

# 🔻 Approach 1: Single Queue, Costly Push (Most Popular)

### 🔸 Idea:

- Enqueue new element
    
- Then rotate all previous elements to the back  
    → Ensures the newest element is always at front (acts like a stack top)
    

---

### ✅ Java Code

```java
class MyStack {
    Queue<Integer> q = new LinkedList<>();

    public void push(int x) {
        q.offer(x);
        int size = q.size();
        while (size-- > 1) {
            q.offer(q.poll()); // rotate all elements except new one
        }
    }

    public int pop() {
        return q.poll();
    }

    public int top() {
        return q.peek();
    }

    public boolean empty() {
        return q.isEmpty();
    }
}
```

---

### ⏱ Time & Space:

|Operation|Time|
|---|---|
|Push|O(n)|
|Pop|O(1) ✅|
|Top|O(1) ✅|
|Empty|O(1)|
|Space|O(n)|

---

# 🔻 Approach 2: Two Queues, Costly Pop (Less Preferred)

### 🔸 Idea:

- Maintain two queues: `q1` (main), `q2` (helper)
    
- On pop: transfer elements from `q1` to `q2` until last, return last
    

---

### ✅ Java Code

```java
class MyStack {
    Queue<Integer> q1 = new LinkedList<>();
    Queue<Integer> q2 = new LinkedList<>();

    public void push(int x) {
        q1.offer(x);
    }

    public int pop() {
        while (q1.size() > 1) {
            q2.offer(q1.poll());
        }
        int top = q1.poll();
        Queue<Integer> temp = q1;
        q1 = q2;
        q2 = temp;
        return top;
    }

    public int top() {
        int res = pop();
        q1.offer(res);  // restore
        return res;
    }

    public boolean empty() {
        return q1.isEmpty();
    }
}
```

---

### ⏱ Time & Space:

|Operation|Time|
|---|---|
|Push|O(1) ✅|
|Pop|O(n)|
|Top|O(n)|
|Space|O(n)|

---

## ✅ Summary

|Approach|Push|Pop|Space|Notes|
|---|---|---|---|---|
|**Single Queue**|O(n)|O(1)|O(n)|✅ Optimal for frequent pops|
|Two Queues|O(1)|O(n)|O(n)|Easier to understand|

---

## 🔗 Leetcode Link

- [Leetcode 225 – Implement Stack using Queues](https://leetcode.com/problems/implement-stack-using-queues/)
    

---

## 🧠 Follow-up Variants

- **Queue using Stacks** (Leetcode 232)
    
- **Design Min Stack**
    
- **Implement Stack with O(1) `getMin()`**
    

---

Would you like:

- Reusable class templates for these problems?
    
- A **Stack using Deque** version as a bonus (Java built-in support)?