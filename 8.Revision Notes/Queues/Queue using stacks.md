Here are the **full notes** for **Leetcode 232 – Implement Queue using Stacks**, covering:

- Problem overview
    
- All valid approaches: brute force (costly `push`), optimal (costly `pop`)
    
- Detailed Java code
    
- Stack traces and dry runs
    
- Time/space complexity comparisons
    
- Interview trade-offs
    

---

# 📘 Leetcode 232 – Implement Queue using Stacks

---

## ✅ Problem Statement

> Implement a **first in, first out (FIFO)** queue using only **two stacks**.  
> You must support:

- `push(x)`: Enqueue
    
- `pop()`: Dequeue
    
- `peek()`: Front of the queue
    
- `empty()`: Is the queue empty?
    

---

## 🔍 Constraints

- Only standard stack operations allowed: `push`, `pop`, `peek`, `isEmpty`
    
- Must simulate **FIFO behavior**
    
- Optimize for **amortized O(1)** time complexity
    

---

# ⚙️ Approach 1 – Costly Push (Brute Force)

---

### 💡 Idea:

- Use one stack (`stack`) to maintain queue in **reversed order** — top is front of queue.
    
- On every `push()`, **reverse the stack** into a temp stack, insert the new element at bottom, reverse back.
    

---

### ✅ Java Code

```java
class MyQueue {
    Stack<Integer> stack = new Stack<>();

    public void push(int x) {
        Stack<Integer> temp = new Stack<>();
        while (!stack.isEmpty()) {
            temp.push(stack.pop());
        }
        stack.push(x);
        while (!temp.isEmpty()) {
            stack.push(temp.pop());
        }
    }

    public int pop() {
        return stack.pop();
    }

    public int peek() {
        return stack.peek();
    }

    public boolean isEmpty() {
        return stack.isEmpty();
    }
}
```

---

### 🔁 Dry Run

```text
push(1): stack = [1]
push(2): temp = [1] → stack = [2,1]
pop():    return 1
```

---

### ⏱ Time Complexity

|Operation|Time|
|---|---|
|`push()`|O(n)|
|`pop()`|O(1)|
|`peek()`|O(1)|
|`empty()`|O(1)|

---

## ⚙️ Approach 2 – ✅ Optimal Approach (Costly Pop/Peek)

---

### 💡 Idea:

- Use **two stacks**:
    
    - `inStack` for pushing new elements
        
    - `outStack` for popping/peeking
        
- On `pop()`/`peek()`:
    
    - If `outStack` is empty → transfer all elements from `inStack` (reverse them)
        
    - Else → operate directly on `outStack`
        

This is the most efficient solution in **amortized O(1)**.

---

### ✅ Java Code

```java
class MyQueue {
    Stack<Integer> inStack = new Stack<>();
    Stack<Integer> outStack = new Stack<>();

    public void push(int x) {
        inStack.push(x);
    }

    public int pop() {
        shiftStacks();
        return outStack.pop();
    }

    public int peek() {
        shiftStacks();
        return outStack.peek();
    }

    public boolean isEmpty() {
        return inStack.isEmpty() && outStack.isEmpty();
    }

    private void shiftStacks() {
        if (outStack.isEmpty()) {
            while (!inStack.isEmpty()) {
                outStack.push(inStack.pop());
            }
        }
    }
}
```

---

### 🔁 Dry Run

```text
push(1): inStack = [1], outStack = []

push(2): inStack = [1, 2]

peek(): shiftStacks() → outStack = [2, 1] → return 1

pop():  outStack.pop() = 1

peek(): return 2
```

---

### ⏱ Time Complexity

|Operation|Time|Why?|
|---|---|---|
|`push()`|O(1)|Plain push|
|`pop()`|Amortized O(1)|Shift only when needed (1-time reversal)|
|`peek()`|Amortized O(1)|Same as pop|
|`empty()`|O(1)|Simple check|

---

# 📊 Comparison Table

|Approach|push()|pop()|peek()|Space|Use Case|
|---|---|---|---|---|---|
|Brute (costly push)|O(n)|O(1)|O(1)|O(n)|Easy to write, not optimal|
|✅ Optimal (costly pop)|O(1)|O(1)*|O(1)*|O(n)|Best for interviews / real use|

* Amortized

---

# ⚠️ Common Pitfalls

|Mistake|Fix|
|---|---|
|Forgetting to check if `outStack` empty|Always call `shiftStacks()` before pop/peek|
|Trying to use a single stack|Won’t work unless you reverse on every push (costly)|
|Using `queue` in Java instead of stack|Only stack operations are allowed per problem constraints|

---

# 🔗 Related Problems

|Problem|Type|
|---|---|
|Leetcode 225 – Implement Stack using Queues|Reverse problem|
|Leetcode 346 – Moving Average|Queue simulation|
|Leetcode 933 – Recent Calls|Simple queue usage|
|Leetcode 1700 – Students/Sandwiches|Queue simulation|

---

# ✅ Summary

|Core Idea|Use 2 stacks to reverse LIFO → FIFO behavior|
|---|---|
|Optimal Strategy|`inStack` for push, `outStack` for pop/peek|
|Time Efficiency|Amortized O(1) for all operations|
|Space|O(n), using two stacks|
|Interview-Ready|Yes – common design question|

---

Would you like:

- A **JUnit test class** for both approaches?
    
- A **PDF or Markdown sheet** for quick revision?
    
- A challenge to **extend this to deque using stacks**?
    

Let me know — I’ll build it for you.