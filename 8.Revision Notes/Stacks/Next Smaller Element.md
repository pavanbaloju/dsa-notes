Here’s your complete, **interview-focused** guide on the **Next Smaller Element (NSE)** — from brute force to optimal with code, dry runs, visual explanation, and real-world problems.

---

# 📘 Next Smaller Element (NSE) – Full Notes

---

## ✅ Problem Statement

> Given an array `nums[]`, for each element, find the **next smaller element to its right**.  
> If no such element exists, return `-1`.

---

### 🔸 Example:

```text
Input:  [4, 5, 2, 10, 8]
Output: [2, 2, -1, 8, -1]

Input:  [1, 3, 0, 2, 5]
Output: [0, 0, -1, -1, -1]
```

---

## 🔁 Problem Pattern

This is a **Monotonic Stack** problem — just like Next Greater Element, but reversed logic.

We need:

- A **monotonic increasing stack** (top is smallest)
    
- Traverse **right to left**
    

---

## 🧠 Real-Life Analogy

Imagine you’re looking at building heights, and for each one, you want to find the **first smaller building on its right**.  
You **ignore (pop) all taller buildings**, and the first shorter one you find is your answer.

---

# ⛔ Brute Force Approach – O(n²)

### 🔸 Idea:

For each element, scan the rest of the array to its right until you find a smaller element.

### ✅ Java Code:

```java
public int[] nextSmallerElementBrute(int[] nums) {
    int n = nums.length;
    int[] res = new int[n];

    for (int i = 0; i < n; i++) {
        res[i] = -1;
        for (int j = i + 1; j < n; j++) {
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

### ⏱ Complexity:

- Time: O(n²)
    
- Space: O(1)
    

---

# ✅ Optimal Approach – Monotonic Stack

### 🔸 Idea:

- Traverse the array from **right to left**
    
- Maintain a **stack in increasing order**
    
- Remove all elements that are **greater than or equal** to the current element
    

---

### ✅ Java Code:

```java
public int[] nextSmallerElement(int[] nums) {
    int n = nums.length;
    int[] res = new int[n];
    Stack<Integer> stack = new Stack<>();

    for (int i = n - 1; i >= 0; i--) {
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

Input: `[4, 5, 2, 10, 8]`

```
i = 4 → nums[4] = 8 → stack = []         → res[4] = -1 → push(8)
i = 3 → nums[3] = 10 → stack = [8]       → res[3] = 8 → push(10)
i = 2 → nums[2] = 2 → pop(10), pop(8)    → res[2] = -1 → push(2)
i = 1 → nums[1] = 5 → stack = [2]        → res[1] = 2 → push(5)
i = 0 → nums[0] = 4 → pop(5)             → res[0] = 2 → push(4)
```

✅ Final Output: `[2, 2, -1, 8, -1]`

---

## ⏱ Complexity:

- Time: O(n)
    
- Space: O(n) for stack
    

Each element is pushed/popped **at most once**.

---

# 📦 Template Recap

|Problem|Stack Type|Traverse|Condition|
|---|---|---|---|
|**Next Smaller**|Increasing Stack|Right → Left|`while (stack.peek() >= val)`|
|**Next Greater**|Decreasing Stack|Right → Left|`while (stack.peek() <= val)`|

---

# 🧠 Edge Cases

|Input|Output|Notes|
|---|---|---|
|[1]|[-1]|No elements to the right|
|[5, 4, 3]|[4, 3, -1]|Strictly decreasing|
|[1, 2, 3]|[-1, -1, -1]|Strictly increasing|
|[2, 2, 2]|[-1, -1, -1]|Equal elements, all same|

---

# 🔄 Variants

### 📌 Indexed Version (return index of next smaller)

Use a `Stack<Integer>` to store **indices** instead of values.

---

### 📌 Circular Version (wrap around like Leetcode 503)

Use `i % n` and loop from `2n-1` to `0`.

---

### 📌 Distance to next smaller (Stock Span variant)

Use index difference: `res[i] = stack.peek() - i`

---

# 🔗 Related Problems

|Problem ID|Name|Variation|
|---|---|---|
|Leetcode 496|Next Greater Element I|NGE|
|Leetcode 503|Next Greater Element II (Circular)|Circular NGE|
|Leetcode 739|Daily Temperatures|Indexed NGE|
|Leetcode 84|Largest Rectangle in Histogram|NSE + span computation|
|Leetcode 85|Max Rectangle in Binary Matrix|2D NSE problem|
|Leetcode 901|Online Stock Span|Previous Smaller/Greater|

---

# 📌 Summary Table

|Feature|Detail|
|---|---|
|Pattern|Monotonic Increasing Stack|
|Traverse Direction|Right → Left|
|Comparison|`stack.peek() >= nums[i]`|
|Optimal Time Complexity|O(n)|
|Space|O(n)|

---

## Would You Like?

- 📘 PDF version of this?
    
- 🎯 A revision deck of **20 quick NGE/NSE questions**?
    
- ✏️ Extension into **histogram/rainwater** using NSE logic?
    

Just say the word, and I’ll generate it!