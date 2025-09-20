Here's the **full notes on Next Greater Element (NGE)** — complete with concepts, patterns, dry run, brute to optimal approaches, and Java code.

---

# 📘 Next Greater Element (NGE) – Full Notes

---

## ✅ Problem Statement

> Given an array `nums`, for each element, find the **next greater element** to its **right**.  
> If no such element exists, return `-1`.

---

### 🔸 Example

```text
Input:  [2, 1, 2, 4, 3]
Output: [4, 2, 4, -1, -1]

Input:  [1, 3, 2, 4]
Output: [3, 4, 4, -1]
```

---

## 🔁 Problem Pattern

- It’s a **Monotonic Stack** problem.
    
- Specifically: **Monotonic Decreasing Stack**
    
- Traverse from **right to left**
    
- Remove all elements from stack that are **less than or equal** to current element
    

---

## 🧱 Real-Life Analogy

Imagine you’re walking down a row of people from right to left. You want to find **the first taller person to your right** for everyone.  
Instead of checking everyone, you **ignore all people shorter than you** (pop from the stack), and the first taller one you find is your answer.

---

# ⛔ Approach 1: Brute Force (Nested Loops)

### ✅ Logic

- For every element, loop to the right and find the first greater value.
    

### ✅ Java Code

```java
public int[] nextGreaterElementBrute(int[] nums) {
    int n = nums.length;
    int[] res = new int[n];

    for (int i = 0; i < n; i++) {
        res[i] = -1;
        for (int j = i + 1; j < n; j++) {
            if (nums[j] > nums[i]) {
                res[i] = nums[j];
                break;
            }
        }
    }

    return res;
}
```

### ⏱ Time: O(n²)

### Space: O(1)

---

# ✅ Approach 2: Optimal Using Monotonic Stack

### 🔸 Idea

- Use a **stack** to store elements in **decreasing order**
    
- Traverse from **right to left**
    
- For each element:
    
    - Pop smaller/equal elements (they can’t be NGE)
        
    - Top of stack is next greater (if stack is not empty)
        
    - Push current element into stack
        

---

### ✅ Java Code

```java
public int[] nextGreaterElement(int[] nums) {
    int n = nums.length;
    int[] res = new int[n];
    Stack<Integer> stack = new Stack<>();

    for (int i = n - 1; i >= 0; i--) {
        while (!stack.isEmpty() && stack.peek() <= nums[i]) {
            stack.pop();
        }
        res[i] = stack.isEmpty() ? -1 : stack.peek();
        stack.push(nums[i]);
    }

    return res;
}
```

---

## 🔁 Dry Run

For: `[2, 1, 2, 4, 3]`

```text
i = 4, nums[i]=3 → stack=[],      res[4]=-1, push(3)
i = 3, nums[i]=4 → pop 3,         res[3]=-1, push(4)
i = 2, nums[i]=2 → stack=[4],     res[2]=4,  push(2)
i = 1, nums[i]=1 → stack=[4,2],   res[1]=2,  push(1)
i = 0, nums[i]=2 → pop 1,2        stack=[4], res[0]=4, push(2)
```

Final result: `[4, 2, 4, -1, -1]`

---

### ⏱ Time: O(n)

### Space: O(n)

---

## 🧠 Edge Cases

|Input|Output|Notes|
|---|---|---|
|[1]|[-1]|No next elements|
|[2,1]|[-1, -1]|Decreasing order|
|[1,2,3]|[2,3,-1]|Ascending order|
|[3,2,1]|[-1,-1,-1]|No greater to the right|

---

## 🔁 Circular Array Variant (Leetcode 503)

In circular arrays, elements can wrap around — simulate two passes.

### 🔸 Java Code

```java
public int[] nextGreaterElements(int[] nums) {
    int n = nums.length;
    int[] res = new int[n];
    Arrays.fill(res, -1);
    Stack<Integer> stack = new Stack<>();

    for (int i = 2 * n - 1; i >= 0; i--) {
        int idx = i % n;
        while (!stack.isEmpty() && stack.peek() <= nums[idx]) {
            stack.pop();
        }
        if (i < n) {
            res[idx] = stack.isEmpty() ? -1 : stack.peek();
        }
        stack.push(nums[idx]);
    }

    return res;
}
```

---

## 📦 Variations

|Problem|Change|
|---|---|
|Return **index** instead of value|Stack stores indices|
|Return **distance to greater**|Subtract indices|
|**Next smaller element**|Flip stack condition|
|**Previous greater element**|Traverse left → right|
|**Circular array**|Loop from `2n - 1` to `0`|

---

## 📌 Summary

|Strategy|Details|
|---|---|
|Pattern|Monotonic Decreasing Stack|
|Direction|Right → Left|
|Time Complexity|O(n)|
|Space Complexity|O(n) for stack|
|Comparison logic|`while stack.peek() <= nums[i]`|

---

## 🧠 Tips

- Always **clear out smaller elements** that are useless
    
- **Stack top is the next greater**, if any
    
- **Each element is pushed and popped at most once**
    

---

## 🔗 Practice Problems

|Leetcode ID|Title|Variation|
|---|---|---|
|496|Next Greater Element I|1 array|
|503|Next Greater Element II|Circular array|
|1019|Next Greater Node in LinkedList|Linked list|
|739|Daily Temperatures|Return distance|
|901|Stock Span|Previous greater|
|84|Largest Rectangle in Histogram|NSE + Span|

---

Would you like me to give:

- Practice sheet for all 4 variations (NGE/NSE/PGE/PSE)?
    
- Monotonic stack-based problems grouped by difficulty?
    
- Diagrams or Java template notebook?
    

Let me know and I’ll set it up.