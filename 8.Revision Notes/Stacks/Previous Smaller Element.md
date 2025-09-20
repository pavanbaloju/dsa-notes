Here are the **full notes on Previous Smaller Element (PSE)** — including problem intuition, dry run, brute to optimal solutions, Java code templates, real-world variants, and key applications.

---

# 📘 Previous Smaller Element (PSE) – Full Notes

---

## ✅ Problem Statement

> Given an array `nums[]`, for each element, find the **previous smaller element** to its **left**.  
> If no such element exists, return `-1`.

---

### 🔸 Example:

```text
Input:  [4, 5, 2, 10, 8]
Output: [-1, 4, -1, 2, 2]

Input:  [1, 3, 0, 2, 5]
Output: [-1, 1, -1, 0, 2]
```

---

## 🔁 Problem Pattern

This is a **Monotonic Stack** problem. Specifically:

- Traverse from **left to right**
    
- Use a **Monotonic Increasing Stack** (top has the smallest values)
    
- Pop values **greater than or equal** to the current element
    

---

## 🧠 Intuition

Imagine walking through a sequence of numbers. For each one, ask:

> “Who was the last number to my left that was smaller than me?”

If someone was larger, they can't help you — so forget them (pop from stack). The first smaller one left is your answer.

---

# ⛔ Brute Force Approach – O(n²)

### 🔸 Logic:

For each element, check to the **left** for the first smaller value.

### ✅ Java Code:

```java
public int[] previousSmallerBrute(int[] nums) {
    int n = nums.length;
    int[] res = new int[n];

    for (int i = 0; i < n; i++) {
        res[i] = -1;
        for (int j = i - 1; j >= 0; j--) {
            if (nums[j] < nums[i]) {
                res[i] = nums[j];
                break;
            }
        }
    }

    return res;
}
```

---

### ⏱ Time: O(n²)

### Space: O(1)

---

# ✅ Optimal Approach – Monotonic Stack

### 🔸 Logic:

- Traverse from **left to right**
    
- Stack maintains elements in **increasing order**
    
- Before pushing the current element, **remove larger/equal elements**
    
- The top of the stack is now the previous smaller (if any)
    

---

### ✅ Java Code:

```java
public int[] previousSmallerElement(int[] nums) {
    int n = nums.length;
    int[] res = new int[n];
    Stack<Integer> stack = new Stack<>();

    for (int i = 0; i < n; i++) {
        while (!stack.isEmpty() && stack.peek() >= nums[i]) {
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

For: `[4, 5, 2, 10, 8]`

```
i = 0 → nums[0] = 4 → stack = []         → res[0] = -1 → push(4)
i = 1 → nums[1] = 5 → stack = [4]        → res[1] = 4  → push(5)
i = 2 → nums[2] = 2 → pop 5, pop 4       → res[2] = -1 → push(2)
i = 3 → nums[3] = 10 → stack = [2]       → res[3] = 2  → push(10)
i = 4 → nums[4] = 8 → pop 10 → stack=[2] → res[4] = 2  → push(8)
```

✅ Final Output: `[-1, 4, -1, 2, 2]`

---

## ⏱ Complexity

- Time: O(n)
    
- Space: O(n) for stack
    

Each element is **pushed and popped once**, so total operations = O(n)

---

# 📦 Template Recap

|Problem|Traverse|Stack Type|Comparison Logic|
|---|---|---|---|
|Previous Smaller Element|Left → Right|Monotonic Increasing|`stack.peek() >= nums[i]`|

---

# 🧠 Edge Cases

|Input|Output|Notes|
|---|---|---|
|[1]|[-1]|No previous elements|
|[2, 2, 2]|[-1, -1, -1]|All elements same|
|[1, 2, 3]|[-1, 1, 2]|Strictly increasing|
|[5, 4, 3]|[-1, -1, -1]|Strictly decreasing|

---

# 🔄 Variants

### 📌 Return Index Instead of Value

- Push **indices** into the stack instead of values
    
- Use: `nums[stack.peek()]` when comparing
    
- Set result: `res[i] = stack.isEmpty() ? -1 : stack.peek()`
    

---

### 📌 Return Distance to Previous Smaller

```java
res[i] = stack.isEmpty() ? 0 : i - stack.peek();
```

Used in:

- Stock Span problems
    
- Histogram bar width calculation
    

---

# 🔗 Related Problems

|Problem ID|Title|Variation Type|
|---|---|---|
|Leetcode 84|Largest Rectangle in Histogram|NSE + PSE used|
|Leetcode 901|Online Stock Span|Return index span|
|Leetcode 496|Next Greater Element I|Right side instead|
|Leetcode 503|Next Greater Element II|Circular + next greater|
|Leetcode 1475|Final Prices With a Special Discount|NSE variant|

---

# 📌 Summary

|Feature|Value|
|---|---|
|Stack Type|Monotonic Increasing Stack|
|Traverse Direction|Left → Right|
|Comparison Logic|`stack.peek() >= nums[i]`|
|Time Complexity|O(n)|
|Space Complexity|O(n)|

---

# 🧠 Monotonic Stack Family

|Name|Traverse|Stack Type|Use Case|
|---|---|---|---|
|Next Greater Element (NGE)|Right → Left|Monotonic Decreasing|Next higher value|
|Next Smaller Element (NSE)|Right → Left|Monotonic Increasing|Next lower value|
|Previous Greater (PGE)|Left → Right|Monotonic Decreasing|Previous higher value|
|Previous Smaller (PSE)|Left → Right|Monotonic Increasing|Previous lower value|

---

Would you like:

- A consolidated PDF of all 4 (NGE/NSE/PGE/PSE) with visual examples?
    
- Practice problems categorized by difficulty?
    
- Monotonic Stack + Indexed span templates (for histogram, daily temps, etc)?
    

Just say the word, and I’ll prep them for you.