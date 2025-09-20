Here are your **full interview-ready notes on Previous Greater Element (PGE)** — covering brute to optimal approaches, dry run, code templates, and real-world applications.

---

# 📘 Previous Greater Element (PGE) – Full Notes

---

## ✅ Problem Statement

> Given an array `nums[]`, for each element, find the **previous greater element to its left**.  
> If no such element exists, return `-1`.

---

### 🔸 Example:

```text
Input:  [4, 5, 2, 10, 8]
Output: [-1, -1, 5, -1, 10]

Input:  [1, 3, 0, 2, 5]
Output: [-1, -1, 3, 3, -1]
```

---

## 🔁 Problem Pattern

This is a **Monotonic Stack** problem.

- Traverse from **left to right**
    
- Maintain a **monotonic decreasing stack** (top is smallest among previous greater)
    
- Pop all elements that are **less than or equal** to current element
    

---

## 🧠 Real-Life Analogy

You're walking left to right through a group of people. For each person, you want to know:

- “Who was the last taller person I passed?”
    

If someone is shorter than you, they **can’t be a valid answer** — remove them from memory (pop the stack).

---

# ⛔ Brute Force Approach – O(n²)

### 🔸 Logic:

Loop from `i-1` to `0` for every element and return the first element greater than it.

### ✅ Java Code:

```java
public int[] previousGreaterBrute(int[] nums) {
    int n = nums.length;
    int[] res = new int[n];

    for (int i = 0; i < n; i++) {
        res[i] = -1;
        for (int j = i - 1; j >= 0; j--) {
            if (nums[j] > nums[i]) {
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
    
- Maintain a **monotonic decreasing stack** (`stack.peek() <= nums[i] → pop`)
    
- The stack top (if any) is the **previous greater**
    

---

### ✅ Java Code:

```java
public int[] previousGreaterElement(int[] nums) {
    int n = nums.length;
    int[] res = new int[n];
    Stack<Integer> stack = new Stack<>();

    for (int i = 0; i < n; i++) {
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

Input: `[4, 5, 2, 10, 8]`

```
i = 0 → nums[0] = 4 → stack = []          → res[0] = -1 → push(4)
i = 1 → nums[1] = 5 → pop(4)              → res[1] = -1 → push(5)
i = 2 → nums[2] = 2 → stack = [5]         → res[2] = 5  → push(2)
i = 3 → nums[3] = 10 → pop(2), pop(5)     → res[3] = -1 → push(10)
i = 4 → nums[4] = 8 → stack = [10]        → res[4] = 10 → push(8)
```

✅ Output: `[-1, -1, 5, -1, 10]`

---

## ⏱ Complexity

- Time: O(n)
    
- Space: O(n) (for stack)
    

Each element is pushed and popped **at most once**.

---

# 📦 Template Recap

|Problem|Stack Type|Traverse|Comparison Logic|
|---|---|---|---|
|**Previous Greater**|Decreasing Stack|Left → Right|`stack.peek() <= nums[i]`|
|**Previous Smaller**|Increasing Stack|Left → Right|`stack.peek() >= nums[i]`|

---

# 🧠 Edge Cases

|Input|Output|Notes|
|---|---|---|
|[1]|[-1]|No left elements|
|[5, 4, 3]|[-1, 5, 4]|Decreasing order|
|[1, 2, 3]|[-1, 1, 2]|Increasing order|
|[2, 2, 2]|[-1, -1, -1]|Equal elements|

---

# 🔄 Variants

### 📌 Return Index Instead of Value

Just push **indices** to the stack and use `nums[stack.peek()]` for value.

---

### 📌 Return Distance to Previous Greater

```java
res[i] = stack.isEmpty() ? 0 : i - stack.peek();
```

---

# 🔗 Related Problems

|Leetcode ID|Problem Name|Variation|
|---|---|---|
|84|Largest Rectangle in Histogram|Use PGE and NSE for span calc|
|901|Online Stock Span|Use Previous Greater Index|
|503|Next Greater Element II|NGE circular|
|496|Next Greater Element I|Basic NGE|

---

# 📌 Summary

|Feature|Value|
|---|---|
|Stack Type|Monotonic Decreasing|
|Traverse Direction|Left → Right|
|Comparison|`while stack.peek() <= nums[i]`|
|Time Complexity|O(n)|
|Space Complexity|O(n)|

---

# 🚀 Monotonic Stack Family

|Name|Traverse|Stack Type|
|---|---|---|
|Next Greater Element|Right → L|Decreasing|
|Next Smaller Element|Right → L|Increasing|
|Previous Greater Element|Left → R|Decreasing|
|Previous Smaller Element|Left → R|Increasing|

---

Would you like:

- A **side-by-side comparison sheet** of all 4 variations?
    
- A set of **5 handpicked problems** to master PGE?
    
- Java template with **indexed spans** (for histogram)?
    

Let me know, and I’ll set that up for you.