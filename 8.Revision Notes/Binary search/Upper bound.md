### **Upper Bound – Binary Search (Revision Notes)**

---

## **1️⃣ What is Upper Bound?**

The **upper bound** of a target `x` in a **sorted array** is the **smallest index `i`** such that:

```plaintext
nums[i] > x
```

- If `x` **exists** in `nums[]`, **upper bound is the index of the first element greater than `x`**.
- If `x` **does not exist**, **upper bound is where `x` would be inserted to maintain order**.
- If `x` **is greater than all elements**, return `n` (insert at the end).

✅ **Upper Bound is useful for counting occurrences (`upperBound - lowerBound`).**

---

## **2️⃣ Key Idea – Binary Search for First `nums[i] > target`**

- Instead of finding an exact match, we find the **smallest index** where `nums[i] > target`.
- If `nums[mid] > target`, move **left** (`right = mid`).
- If `nums[mid] ≤ target`, move **right** (`left = mid + 1`).
- The answer will be at `left`.

✅ **Time Complexity:** **O(log n)**  
✅ **Space Complexity:** **O(1) (Iterative Approach)**

---

## **3️⃣ Binary Search Approach (Iterative)**

### **Algorithm Steps:**

1. Initialize **`left = 0`** and **`right = n`** (**Note: `n`, not `n - 1`**).
2. Compute `mid = left + (right - left) / 2`.
3. **If `nums[mid] > target`**, move **left** (`right = mid`).
4. **Else**, move **right** (`left = mid + 1`).
5. When `left == right`, return `left` (upper bound index).

---

## **4️⃣ Code Implementation (Iterative)**

```java
public int upperBound(int[] nums, int target) {
    int left = 0, right = nums.length;

    while (left < right) { // Search space is [left, right)
        int mid = left + (right - left) / 2;

        if (nums[mid] > target) {
            right = mid; // Move left to find first greater element
        } else {
            left = mid + 1; // Move right
        }
    }

    return left; // Upper bound index
}
```

✅ **Why `right = mid` and not `mid - 1`?**

- `mid` could be the **first index** where `nums[i] > target`, so we **include it** in the search.

✅ **Why return `left`?**

- `left` will always point to the **smallest index where `nums[i] > target`**.

---

## **5️⃣ Example Walkthrough**

🔹 **Example 1 – Target Exists**

```plaintext
Input: nums = [1, 2, 4, 4, 6, 8], target = 4
```

|Iteration|`left`|`right`|`mid`|`nums[mid]`|Action|
|---|---|---|---|---|---|
|1|`0`|`6`|`3`|`4`|Move right (`left = 4`)|
|2|`4`|`6`|`5`|`8`|Move left (`right = 5`)|
|3|`4`|`5`|`4`|`6`|Move left (`right = 4`)|

✅ **Output:** `4` (First element greater than `4` is at index `4`)

---

🔹 **Example 2 – Target Not Found, Insert Position Needed**

```plaintext
Input: nums = [1, 2, 4, 4, 6, 8], target = 5
```

|Iteration|`left`|`right`|`mid`|`nums[mid]`|Action|
|---|---|---|---|---|---|
|1|`0`|`6`|`3`|`4`|Move right (`left = 4`)|
|2|`4`|`6`|`5`|`8`|Move left (`right = 5`)|
|3|`4`|`5`|`4`|`6`|Move left (`right = 4`)|

✅ **Output:** `4` (Insert `5` at index `4`)

---

## **6️⃣ Edge Cases & Handling**

| **Case**                     | **Example**                       | **Handling**                  |
| ---------------------------- | --------------------------------- | ----------------------------- |
| **Target is Smallest**       | `nums = [5,10,15]`, `target = 1`  | Returns `0` (Insert at start) |
| **Target is Largest**        | `nums = [5,10,15]`, `target = 20` | Returns `3` (Insert at end)   |
| **All Elements are Smaller** | `nums = [1,2,3]`, `target = 4`    | Returns `3`                   |
| **All Elements are Greater** | `nums = [5,6,7]`, `target = 4`    | Returns `0`                   |
| **Single Element Array**     | `nums = [10]`, `target = 10`      | Returns `1`                   |
|                              |                                   |                               |

✅ **Works for all edge cases without modification.**

---

## **7️⃣ Recursive Approach (Alternative)**

```java
public int upperBoundRecursive(int[] nums, int left, int right, int target) {
    if (left >= right) return left;

    int mid = left + (right - left) / 2;

    if (nums[mid] > target) return upperBoundRecursive(nums, left, mid, target);
    else return upperBoundRecursive(nums, mid + 1, right, target);
}

public int upperBound(int[] nums, int target) {
    return upperBoundRecursive(nums, 0, nums.length, target);
}
```

✅ **Drawback:** Uses **O(log n) stack space**, making **iterative preferred**.

---

## **8️⃣ Why Binary Search is Ideal Here?**

🔹 **Without Binary Search (Linear Search O(n))**

- **Scanning every element** is **too slow for large `n`**.
- **Worst Case:** Searching `x = 500,000` in `nums[0...999,999]` requires **500,000** comparisons.

🔹 **With Binary Search (O(log n))**

- **Halves the search space** each step.
- **Example:** `n = 1,000,000`, only **20 checks** (`log₂ 1,000,000 ≈ 20`).

✅ **Binary Search is optimal for upper bound problems.**

---

## **9️⃣ Similar Problems & Variations**

|**Problem**|**Concept**|**Leetcode**|
|---|---|---|
|**Find First and Last Occurrence in Sorted Array**|Lower & Upper Bound Binary Search|**Leetcode 34**|
|**Search Insert Position**|Lower Bound Concept|**Leetcode 35**|
|**Find Minimum in Rotated Sorted Array**|Binary Search on Rotated Arrays|**Leetcode 153**|

---

## **🔟 Summary & Key Takeaways**

✅ **Use Binary Search (`O(log n)`)** to find the first `nums[i] > target`.  
✅ **Return `left` after the loop**, since it stores the **upper bound index**.  
✅ **Adjust `right = mid` instead of `mid - 1`** to ensure we don’t miss `mid`.  
✅ **Handles all edge cases, including inserting at the start, middle, or end**.

Would you like **a breakdown of another Binary Search variation (e.g., rotated search, binary search on answer)?** 🚀