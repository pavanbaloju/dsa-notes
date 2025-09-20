### **Leetcode 704 – Binary Search (Revision Notes)**

---

## **1️⃣ Problem Statement**

You are given a **sorted** array `nums[]` of `n` elements and an integer `target`. Find the **index** of `target` in `nums[]` using **binary search**. If `target` is not found, return `-1`.

🔹 **Constraints:**

- `nums[]` is sorted in **ascending order**.
- `-10⁴ ≤ nums[i], target ≤ 10⁴`
- `1 ≤ nums.length ≤ 10⁴`

---

## **2️⃣ Approach – Binary Search**

🔹 **Key Idea:** Since `nums[]` is sorted, we can apply **Binary Search (O(log n))** instead of **Linear Search (O(n))**.  
🔹 **Steps:**

1. Initialize `left = 0` and `right = n - 1`.
2. Compute `mid = left + (right - left) / 2` (to prevent overflow).
3. Compare `nums[mid]` with `target`:
    - **If `nums[mid] == target`**, return `mid`.
    - **If `nums[mid] < target`**, search **right half** (`left = mid + 1`).
    - **If `nums[mid] > target`**, search **left half** (`right = mid - 1`).
4. Repeat until `left > right`.
5. If `target` is not found, return `-1`.

✅ **Time Complexity:** **O(log n)**  
✅ **Space Complexity:** **O(1)** (Iterative)

---

## **3️⃣ Code Implementation**

### **🔹 Iterative Approach (Recommended)**

```java
public int binarySearch(int[] nums, int target) {
    int left = 0, right = nums.length - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2; // Avoids overflow

        if (nums[mid] == target) return mid;
        else if (nums[mid] < target) left = mid + 1; // Search right half
        else right = mid - 1; // Search left half
    }

    return -1; // Not found
}
```

✅ **Best for iterative solutions (O(1) space)**

---

### **🔹 Recursive Approach**

```java
public int binarySearchRecursive(int[] nums, int left, int right, int target) {
    if (left > right) return -1; // Base case: Not found

    int mid = left + (right - left) / 2;

    if (nums[mid] == target) return mid;
    else if (nums[mid] < target) return binarySearchRecursive(nums, mid + 1, right, target);
    else return binarySearchRecursive(nums, left, mid - 1, target);
}
```

✅ **Uses recursion but has O(log n) space due to stack calls**

---

## **4️⃣ Example Walkthrough**

🔹 **Input:**

```plaintext
nums = [-1, 0, 3, 5, 9, 12], target = 9
```

🔹 **Steps:**

|Iteration|`left`|`right`|`mid`|`nums[mid]`|Action|
|---|---|---|---|---|---|
|1|`0`|`5`|`2`|`3`|Search right (`left = 3`)|
|2|`3`|`5`|`4`|`9`|**Found (Return `4`)**|

🔹 **Output:** `4`

---

## **5️⃣ Edge Cases**

|**Case**|**Example**|**Handling**|
|---|---|---|
|**Element Found**|`nums = [1, 3, 5, 7]`, `target = 5`|Returns index `2`|
|**Element Not Found**|`nums = [1, 3, 5, 7]`, `target = 6`|Returns `-1`|
|**Single Element Array**|`nums = [10]`, `target = 10`|Returns `0`|
|**Empty Array**|`nums = []`, `target = 5`|Returns `-1`|
|**Target is First/Last Element**|`nums = [1, 3, 5, 7, 9]`, `target = 1 or 9`|Searches left or rightmost index|

---

## **6️⃣ Alternative Approaches**

🔹 **Linear Search (O(n))** – **Inefficient for large `n`**  
🔹 **Jump Search (O(√n))** – **Not required here**

✅ **Binary Search is the optimal approach for sorted arrays.**

Would you like **detailed explanations for a variation?** 🚀