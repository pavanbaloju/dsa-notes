### **Types of Sliding Window Techniques**

The **Sliding Window technique** is primarily divided into **two categories** based on whether the window size is fixed or variable:

---

## **1. Fixed-Size Sliding Window**

- The **window size (`k`) is constant** and slides across the array.
- Used when the problem explicitly mentions **subarrays of size `k`**.
- **Common operations:** Compute sums, maximums, minimums, distinct elements, etc.

### **Example Problems:**
1. [[Max or Min sum of subarray of size k]]
2. [[Sum of Minimum and Maximum Elements of All Subarrays of Size K]]
3. [[Count Distinct Elements in Every Window of Size K]]
4. [[Find First Negative Integer in Every K-Size Window]]
5. [[Maximum of Each Subarray of Size K]]
6. [[Sum of Each Subarrays of Size K]]
7. [[Sliding window maximum]]


---

## **2. Variable-Size Sliding Window**

- The **window size changes dynamically** based on the problem constraints.
- Used when we need to **find the longest/shortest subarray satisfying a condition**.

### **Types of Variable-Size Sliding Window Problems:**

|**Type**|**Description**|**Example Problems**|
|---|---|---|
|**Expanding & Contracting**|Expand `end++` and shrink `start++` when condition is violated|✅ Longest subarray with sum ≤ `k`✅ Smallest subarray with sum ≥ `k`✅ Maximize toys within budget `k`|
|**Two-Pointer (Shrink until valid)**|Maintain a valid range and minimize `start`|✅ Longest substring with at most `k` distinct characters✅ Longest repeating character replacement|
|**Binary Search + Sliding Window**|Use binary search on window size + sliding window to validate|✅ Maximum subarray size such that all subarrays have sum ≤ `k`|
1. [[Longest substring without repeating characters]]
2. [[Longest substring with atmost k distinct characters]]
3. [[Minimum size subarray sum]]
4. [[Longest Repeating Character Replacement]]
5. [[Number of Substrings Containing All Three Characters]]
6. [[Count Substrings with At Most K Distinct Characters]]
---

## **3. Special Variants of Sliding Window**

### **A) Monotonic Sliding Window (Using Deque)**

- Used when we need **min/max elements dynamically** in a sliding window.
- **Uses a deque (double-ended queue)** to maintain increasing/decreasing order.
- **Example Problems:**
    - ✅ **Sliding Window Maximum**
    - ✅ **Sliding Window Minimum**
    - ✅ **Sum of minimum and maximum of all subarrays of size `k`**

---

### **B) Sliding Window with Frequency Map (HashMap/Set)**

- Used when **tracking frequency/counts** in a window.
- **Example Problems:**
    - ✅ **Count distinct elements in every window of size `k`**
    - ✅ **Find all anagrams of a pattern in a string**
    - ✅ **Longest substring without repeating characters**

---

### **C) Sliding Window with Two Pointers**

- A variant of variable-size sliding window where both **`start` and `end` pointers move independently** to maintain conditions.
- **Example Problems:**
    - ✅ **Longest subarray with absolute difference ≤ `k`**
    - ✅ **Smallest subarray with sum ≥ `k`**
    - ✅ **Longest substring with at most `k` distinct characters**

---

## **4. Summary of Sliding Window Variations**

|**Type**|**Window Size**|**Common Data Structures Used**|**Use Cases**|
|---|---|---|---|
|**Fixed-Size Sliding Window**|Fixed (`k`)|Array, Deque (for min/max)|Sum, max, min, count in subarrays of size `k`|
|**Variable-Size Sliding Window**|Dynamic (shrinks when condition fails)|Two Pointers, HashMap/Set|Longest/shortest subarray satisfying a condition|
|**Monotonic Sliding Window**|Fixed (`k`)|Deque (Maintains min/max order)|Sliding Window Maximum/Minimum|
|**Sliding Window + Frequency Map**|Fixed or Variable|HashMap, Set|Count distinct elements, anagrams|
|**Sliding Window + Two Pointers**|Variable|Two pointers (`start`, `end`)|Longest subarray/substring problems|

---

### **Final Takeaways**

✅ **Fixed-size sliding window** → Used when `k` is explicitly given.  
✅ **Variable-size sliding window** → Used when we dynamically find a valid subarray/substring.  
✅ **Monotonic Sliding Window** → Used for **range queries (max/min in window)**.  
✅ **Sliding Window + Frequency Map** → Used for **tracking elements** (e.g., distinct counts, anagrams).

Would you like a **detailed breakdown with patterns for each category**?


## References
https://leetcode.com/discuss/post/3722472/sliding-window-technique-a-comprehensive-ix2k/
https://leetcode.com/discuss/post/1773891/sliding-window-technique-and-question-ba-9tt4/