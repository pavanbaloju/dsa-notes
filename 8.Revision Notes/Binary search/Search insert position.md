### **🔹 Search Insert Position – Comprehensive Revision Notes**

This problem is a standard application of **Binary Search**. It requires finding the correct **index** where a given `target` should be **inserted** in a sorted array. If the target already exists in the array, return its index; otherwise, return the **index where it would be placed** while maintaining the sorted order.

---

## **🔹 Problem Statement (Leetcode 35 – Search Insert Position)**

### **📝 Given:**

- A **sorted** array `nums` (in ascending order).
    
- An integer `target` to search.
    

### **🎯 Output:**

- Return the **index** of `target` if found.
    
- If `target` is **not present**, return the **index where it should be inserted** while keeping the array sorted.
    

---

## **🔹 Approach: Using Binary Search**

Binary Search efficiently finds the target or its correct insertion position in **O(log n)** time.

### **🔹 Steps to Solve:**

1. **Initialize Two Pointers:**
    
    - `left = 0` (starting index)
        
    - `right = nums.length - 1` (last index)
        
2. **Binary Search Loop (`while left ≤ right`)**
    
    - Compute **midpoint**:
        
        ```java
        int mid = left + (right - left) / 2;
        ```
        
        - This prevents **integer overflow**.
            
    - **Compare `nums[mid]` with `target`:**
        
        - ✅ **If `nums[mid] == target`** → Return `mid` (target found).
            
        - ✅ **If `nums[mid] < target`** → Search in the **right half** (`left = mid + 1`).
            
        - ✅ **If `nums[mid] > target`** → Search in the **left half** (`right = mid - 1`).
            
3. **Return `left` as the insertion position**
    
    - If the `target` is **not found**, the left pointer (`left`) represents the **correct insertion index**.
        

---

## **🔹 Java Code (Iterative Approach)**

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0, right = nums.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2; // Prevents overflow
            
            if (nums[mid] == target) {
                return mid; // Target found at index mid
            } else if (nums[mid] < target) {
                left = mid + 1; // Search in right half
            } else {
                right = mid - 1; // Search in left half
            }
        }

        return left; // Insertion position
    }
}
```

### **🔹 Dry Run Example**

#### **Example 1**

```plaintext
Input: nums = [1, 3, 5, 6], target = 5
Binary Search Steps:
    mid = (0 + 3) / 2 = 1  → nums[1] = 3 < target
    left = mid + 1 = 2
    mid = (2 + 3) / 2 = 2  → nums[2] = 5 == target
Output: 2
```

#### **Example 2**

```plaintext
Input: nums = [1, 3, 5, 6], target = 2
Binary Search Steps:
    mid = (0 + 3) / 2 = 1  → nums[1] = 3 > target
    right = mid - 1 = 0
    mid = (0 + 0) / 2 = 0  → nums[0] = 1 < target
    left = mid + 1 = 1
Output: 1  (Insert before 3)
```

---

## **🔹 Java Code (Recursive Approach)**

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        return binarySearch(nums, target, 0, nums.length - 1);
    }

    private int binarySearch(int[] nums, int target, int left, int right) {
        if (left > right) return left; // Insertion point

        int mid = left + (right - left) / 2;
        if (nums[mid] == target) return mid;

        if (nums[mid] < target)
            return binarySearch(nums, target, mid + 1, right);
        else
            return binarySearch(nums, target, left, mid - 1);
    }
}
```

✅ **Recursion keeps dividing the search space** but has a higher **space complexity (`O(log n)`)** due to recursive stack calls.

---

## **🔹 Complexity Analysis**

|Approach|Time Complexity|Space Complexity|
|---|---|---|
|**Iterative Binary Search**|`O(log n)`|`O(1)`|
|**Recursive Binary Search**|`O(log n)`|`O(log n)` (recursion stack)|
|**Linear Search (Brute Force)**|`O(n)`|`O(1)`|

🚀 **Binary Search is much more efficient than Linear Search (`O(n)`).**

---

## **🔹 Edge Cases to Consider**

|Case|Example|Expected Output|
|---|---|---|
|**Target Exists**|`[1, 3, 5, 6], target = 5`|`2`|
|**Target is Smallest**|`[2, 3, 5, 6], target = 1`|`0`|
|**Target is Largest**|`[1, 3, 5, 6], target = 7`|`4`|
|**Single Element, Equal to Target**|`[5], target = 5`|`0`|
|**Single Element, Target Less**|`[5], target = 3`|`0`|
|**Single Element, Target Greater**|`[5], target = 8`|`1`|

---

## **🔹 Alternative Approach: Linear Search (Brute Force)**

🔴 **Not Recommended** for large inputs, as it takes `O(n)` time.

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] >= target) return i;
        }
        return nums.length;
    }
}
```

✔ Works for small arrays, but **inefficient for large datasets**.

---

## **🔹 Key Takeaways**

- **Binary Search** is the optimal approach with `O(log n)` time complexity.
    
- **Iterative Binary Search** is preferred due to `O(1)` space complexity.
    
- **Recursive Binary Search** works but uses `O(log n)` extra space.
    
- The `left` pointer represents the **correct insertion index** when the target is not found.
    

---

Would you like a **real-world application** of this problem in databases or search engines? 🚀