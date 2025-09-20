## **🔹 Quick Revision Notes – Search in Rotated Sorted Array (No Duplicates)**

### **Problem Statement**

Given a **rotated sorted array** and a target value, find the target’s index in **O(log N)** time. If not found, return `-1`.

---

### **🔹 Key Observations**

1. **Rotated Sorted Array Property:**
    
    - One half of the array is always **sorted**.
        
2. **Binary Search Modifications:**
    
    - Find `mid = (left + right) / 2`.
        
    - **Check if `mid` is the target**.
        
    - Determine **which half is sorted**:
        
        - If `nums[left] <= nums[mid]`, **left half is sorted**.
            
        - Else, **right half is sorted**.
            
    - Narrow search to the half where the target **must be present**.
        

---

### **🔹 Java Code**

```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0, right = nums.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (nums[mid] == target) return mid; // Found target

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
        return -1; // Target not found
    }
}
```

---

### **🔹 Example Walkthrough**

#### **Example 1**

🔹 **Input:**  
`nums = [4,5,6,7,0,1,2], target = 0`  
🔹 **Steps:**

1. `mid = 3` → `nums[mid] = 7` (Left half sorted)
    
2. `0` is **not** in `[4,5,6,7]`, search right half.
    
3. `mid = 5` → `nums[mid] = 1` (Left half sorted)
    
4. `0` is in `[0,1]`, search left half.
    
5. `mid = 4` → `nums[mid] = 0` ✅ **Found at index `4`**.
    

🔹 **Output:** `4`

---

### **🔹 Complexity Analysis**

- **Time Complexity:** **O(log N)** (Binary search halves the search space).
    
- **Space Complexity:** **O(1)** (Only a few variables are used).
    

---

### **🔹 Edge Cases to Consider**

✅ **Target at Pivot:** Ensure handling of cases like `[3, 4, 5, 1, 2]` where target is `1`.  
✅ **Small Array:** `[1]` or `[1, 3]`.  
✅ **Already Sorted Array:** `[1, 2, 3, 4, 5]`, acts as normal binary search.

---

### **🔹 Summary Table**

|Condition|Action|
|---|---|
|`nums[mid] == target`|Return `mid`|
|Left half (`nums[left] ≤ nums[mid]`) is sorted|Check if `target` is in `[left, mid-1]`|
|Right half is sorted|Check if `target` is in `[mid+1, right]`|

This is a **highly common interview pattern**, so practice well! 🚀