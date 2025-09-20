Here are **comprehensive revision notes** for **Finding the Minimum in a Rotated Sorted Array** using Binary Search.

---

## **🔹 Problem Statement**

Given a rotated sorted array, find the **minimum element**.  
The array was originally sorted in **ascending order**, but then **rotated** at some pivot unknown to you.

### **Example**

```java
Input: nums = [4,5,6,7,0,1,2]
Output: 0
```

---

## **🔹 Key Observations**

1. **Rotation Effect**:
    
    - The **smallest element (pivot)** is the point where the sorted order is **broken**.
        
    - The **right half** (after pivot) is always in sorted order.
        
    - The **left half** (before pivot) has an increasing sequence but contains larger numbers.
        
2. **Binary Search Approach**
    
    - Instead of linear search (O(n)), we use **binary search (O(log n))** to locate the pivot efficiently.
        

---

## **🔹 Binary Search Algorithm**

1. Initialize **left = 0** and **right = n - 1**.
    
2. While `left < right`:
    
    - Compute `mid = (left + right) / 2`
        
    - If `nums[mid] > nums[right]` → **pivot is in right half**, so move `left = mid + 1`
        
    - Else → **pivot is in left half**, so move `right = mid`
        
3. Return `nums[left]` (or `nums[right]`, since `left == right`).
    

---

## **🔹 Why Do We Compare `nums[mid]` with `nums[right]`?**

- The pivot **always has a larger element to its right**.
    
- We use `nums[right]` because it belongs to the sorted half, helping us determine which side to move towards.
    

### **Case 1: `nums[mid] > nums[right]`**

- Pivot is **to the right**.
    
- Example: `[4, 5, 6, 7, 0, 1, 2]`
    
- `mid = 7`, `right = 2`
    
- Since `7 > 2`, **move left to right half** (`left = mid + 1`).
    

### **Case 2: `nums[mid] ≤ nums[right]`**

- Pivot is **at `mid` or in the left half**.
    
- Example: `[4, 5, 6, 0, 1, 2, 3]`
    
- `mid = 0`, `right = 3`
    
- Since `0 < 3`, **move right to mid** (`right = mid`).
    

---

## **🔹 Java Code Implementation**

```java
class Solution {
    public int findMin(int[] nums) {
        int left = 0, right = nums.length - 1;
        
        while (left < right) {
            int mid = left + (right - left) / 2;

            if (nums[mid] > nums[right]) {
                // Minimum is in the right half
                left = mid + 1;
            } else {
                // Minimum is in the left half or at mid
                right = mid;
            }
        }
        return nums[left];  // or nums[right] (both are the same at the end)
    }
}
```

---

## **🔹 Dry Run Example**

### **Example: `[4, 5, 6, 7, 0, 1, 2]`**

|Left|Mid|Right|nums[mid]|nums[right]|Move Left or Right?|
|---|---|---|---|---|---|
|0|3|6|7|2|Left → `mid + 1 = 4`|
|4|5|6|1|2|Right → `mid = 5`|
|4|4|5|0|1|Right → `mid = 4`|

**Final Answer:** `nums[4] = 0`

---

## **🔹 Summary**

- **Time Complexity**: `O(log n)` (Binary Search)
    
- **Why compare `nums[mid]` with `nums[right]`?**
    
    - The pivot has a **larger** element to the right.
        
    - `nums[right]` is always in a sorted section, helping us decide where to move.
        
- **Key Idea**:
    
    - `nums[mid] > nums[right]` → Pivot **right**, move `left = mid + 1`
        
    - `nums[mid] ≤ nums[right]` → Pivot **left or at mid**, move `right = mid`
        

This method efficiently finds the minimum in a rotated sorted array in **logarithmic time**.