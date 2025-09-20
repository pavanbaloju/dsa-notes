## **🔹 Quick Revision Notes – Search in Rotated Sorted Array II (With Duplicates)**

### **🔹 Problem Statement**

Given a **rotated sorted array** that may contain **duplicates**, find the target element's index in **O(log N)** time in the best case. If the target is not found, return `-1`.

---

### **🔹 Key Differences from "Search in Rotated Sorted Array I"**

1. **Duplicates Exist:** Unlike the previous version, the array **can contain duplicate elements**.
    
2. **Ambiguity in Sorted Half:** When `nums[left] == nums[mid] == nums[right]`, we cannot determine whether the left or right half is sorted. In such cases, we **reduce the search space linearly** by moving `left++`.
    

---

### **🔹 Binary Search Approach with Modifications**

1. **Find `mid`** → `mid = (left + right) / 2`.
    
2. **Check if `mid` is the target.**
    
3. **Handle Duplicates:** If `nums[left] == nums[mid] == nums[right]`, increment `left++` and decrement `right--` to shrink the search space.
    
4. **Determine Sorted Half:**
    
    - If `nums[left] ≤ nums[mid]`, the **left half is sorted**.
        
    - Otherwise, the **right half is sorted**.
        
5. **Narrow the Search:**
    
    - If `target` lies within the sorted half, update `left` or `right` accordingly.
        

---

### **🔹 Java Code**

```java
class Solution {
    public boolean search(int[] nums, int target) {
        int left = 0, right = nums.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (nums[mid] == target) return true; // Found target

            // If left, mid, and right are same, move left pointer
            if (nums[left] == nums[mid] && nums[mid] == nums[right]) {
                left++;
                right--;
                continue;
            }

            // Left half is sorted
            if (nums[left] <= nums[mid]) {
                if (nums[left] <= target && target < nums[mid]) {
                    right = mid - 1; // Search in left half
                } else {
                    left = mid + 1; // Search in right half
                }
            }
            // Right half is sorted
            else {
                if (nums[mid] < target && target <= nums[right]) {
                    left = mid + 1; // Search in right half
                } else {
                    right = mid - 1; // Search in left half
                }
            }
        }
        return false; // Target not found
    }
}
```

---

### **🔹 Example Walkthrough**

#### **Example 1**

🔹 **Input:**  
`nums = [2,5,6,0,0,1,2], target = 0`

🔹 **Steps:**

1. `mid = 3` → `nums[mid] = 0` ✅ **Found target, return `true`**
    

🔹 **Output:** `true`

---

### **🔹 Complexity Analysis**

- **Best Case:** **O(log N)** (Normal binary search).
    
- **Worst Case:** **O(N)** (If all elements are the same, we must check linearly).
    
- **Space Complexity:** **O(1)** (Only variables used).
    

---

### **🔹 Edge Cases to Consider**

✅ **All Duplicates:** `[1,1,1,1,1]`, must linearly shrink search space.  
✅ **Target at Pivot:** Ensure handling for `[3, 4, 5, 1, 2, 2, 2]` with `target = 1`.  
✅ **Already Sorted Array:** `[1, 2, 3, 4, 5]`, acts like normal binary search.

---

### **🔹 Summary Table**

|Condition|Action|
|---|---|
|`nums[mid] == target`|Return `true`|
|`nums[left] == nums[mid] == nums[right]`|Increment `left++`, decrement `right--`|
|Left half (`nums[left] ≤ nums[mid]`) is sorted|Check if `target` is in `[left, mid-1]`|
|Right half is sorted|Check if `target` is in `[mid+1, right]`|

This is a **common modification of binary search**, useful when duplicates exist in the array. 🚀