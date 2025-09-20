Here are the **full notes** for **Stock Span Problem** — a classic **Monotonic Stack** question often asked in interviews and used as a base pattern in many variants like Next Greater Element.

---

# 📘 Stock Span Problem: Full Notes

---

## ✅ Problem Statement

> Given a list of daily stock prices, return a list where each element at index `i` is the **span of the stock’s price** on that day — the number of consecutive days before and including the current day where the price was **less than or equal** to today's price.

---

### 🧪 Example

```txt
Input:  prices = [100, 80, 60, 70, 60, 75, 85]
Output:         [1,   1,  1,  2,  1,  4, 6]
```

### 🔍 Explanation:

- Day 0: 100 → span = 1 (no previous price ≥)
    
- Day 1: 80 → span = 1 (only 80)
    
- Day 2: 60 → span = 1
    
- Day 3: 70 → span = 2 (70, 60)
    
- Day 4: 60 → span = 1
    
- Day 5: 75 → span = 4 (75, 60, 70, 60)
    
- Day 6: 85 → span = 6
    

---

## 🧠 Intuition

We want to find **how far back** we can go from index `i` such that all previous prices are **less than or equal** to `prices[i]`.

This is a classic case of **Nearest Greater to Left (NGL)** or **Previous Greater Element (PGE)**.

Use a **Monotonic Decreasing Stack** to keep track of **indices of greater elements**.

---

## ✅ Monotonic Stack Approach

### 🔸 Stack stores: **Pair of (price, index)**

### 🔸 While current price ≥ top of stack → pop

### 🔸 Span = `i - previous greater index`

---

## ✅ Java Code

```java
public int[] calculateSpan(int[] prices) {
    int n = prices.length;
    int[] span = new int[n];
    Stack<Integer> stack = new Stack<>();

    for (int i = 0; i < n; i++) {
        while (!stack.isEmpty() && prices[stack.peek()] <= prices[i]) {
            stack.pop();
        }

        span[i] = stack.isEmpty() ? (i + 1) : (i - stack.peek());
        stack.push(i);
    }

    return span;
}
```

---

## 🔁 Dry Run on `[100, 80, 60, 70, 60, 75, 85]`

|i|Price|Stack (Indices)|Span Calculation|Span|
|---|---|---|---|---|
|0|100|[]|empty → span = 1|1|
|1|80|[0]|top (100) > 80 → span = 1|1|
|2|60|[0, 1]|top (80) > 60 → span = 1|1|
|3|70|[0, 1, 2]|pop 60 → span = 3 - 1 = 2|2|
|4|60|[0, 1, 3]|span = 1|1|
|5|75|[0, 1, 3, 4]|pop 60, 70 → span = 5 - 1 = 4|4|
|6|85|[0, 1, 5]|pop 75, 80 → span = 6 - 0 = 6|6|

---

## ⏱ Time and Space Complexity

|Metric|Value|
|---|---|
|Time|O(n)|
|Space|O(n) for stack|

Each element is pushed and popped **at most once** → amortized O(n)

---

## 🔁 Variant Interpretation as NGE/PGE

- This is a variation of **Previous Greater Element**
    
- Instead of returning the element, we use its **index** to compute span
    
- Same monotonic logic applies
    

---

## 🔄 Alternative (PGE array version)

If you want to store indices of PGE and compute spans later:

```java
for (int i = 0; i < n; i++) {
    while (!stack.isEmpty() && prices[stack.peek()] <= prices[i]) {
        stack.pop();
    }
    pge[i] = stack.isEmpty() ? -1 : stack.peek();
    stack.push(i);
}
```

Then:

```java
span[i] = i - pge[i];
```

---

## 🧠 Common Mistakes

|Mistake|Fix|
|---|---|
|Using values instead of indices|You need **index difference**|
|Not checking empty stack|Default span = `i + 1` if empty|
|Using `>=` instead of `>`|Use `<=` to pop strictly lower|

---

## 🔗 Related Problems

|Problem Name|Type|
|---|---|
|Leetcode 901 – Online Stock Span|Online version, same logic|
|Leetcode 84 – Largest Rectangle|Use of NSE/PSE|
|Leetcode 496 – Next Greater Element|NGE|
|Leetcode 503 – Circular NGE|NGE in circular arrays|

---

## ✅ Summary

|Concept|Value|
|---|---|
|What to find|Days before current ≤ current|
|Data structure|Monotonic decreasing stack|
|Stack stores|Indices of prices|
|Final result|`i - stack.peek()` if not empty, else `i + 1`|

---

Would you like:

- A **PDF cheat sheet** with code and dry run table?
    
- A version for **Leetcode 901 (online)** with class methods?
    
- A **practice worksheet** with similar stack questions?
    

Let me know — I’ll build it for you!