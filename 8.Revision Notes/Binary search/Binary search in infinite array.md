# **Binary Search on Infinite Sorted Arrays**

## **🔹 Problem Statement**

You are given an **infinite sorted array** (or an array where the size is unknown). Find the index of a given target element.

## **🔹 Key Challenges**

- We **do not know the array size**.
    
- We **cannot access the length (`arr.length`)**.
    
- Using standard **binary search is not feasible** since we need `high = arr.length - 1`.
    

---

## **🔹 Key Idea: Exponential Search + Binary Search**

Since we do not know the size, we need to **find an appropriate search boundary first**, and then perform **binary search**.

### **Step 1️⃣ – Finding the Search Boundaries (Exponential Expansion)**

1. Start with `low = 0` and `high = 1`.
    
2. Keep **doubling `high` (`high *= 2`)** until:
    
    - `arr[high] >= target` (potential range found).
        
    - We reach an out-of-bound index (if possible).
        

### **Step 2️⃣ – Apply Standard Binary Search**

- Once the boundary `[low, high]` is found, **apply binary search** in this subarray.
    

---

## **🔹 Code Implementation (Java)**

```java
class Solution {
    public int searchInfiniteSortedArray(int[] arr, int target) {
        int low = 0;
        int high = 1;

        // **Step 1: Find an appropriate search boundary**
        while (high < arr.length && arr[high] < target) {
            low = high; // Move `low` to current `high`
            high *= 2;  // Exponentially expand the boundary
        }

        // **Step 2: Apply binary search within [low, high]**
        return binarySearch(arr, low, Math.min(high, arr.length - 1), target);
    }

    private int binarySearch(int[] arr, int low, int high, int target) {
        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (arr[mid] == target) return mid;
            else if (arr[mid] < target) low = mid + 1;
            else high = mid - 1;
        }
        return -1; // Target not found
    }
}
```

---

## **🔹 Why Exponential Search?**

✅ **Efficient for unknown-sized arrays** – Finds boundary **in O(log K)** where `K` is the target's index.  
✅ **Binary search reduces complexity further** – After boundary detection, binary search takes **O(log K)**.

### **🔹 Time Complexity**

1. **Finding Boundary:** `O(log K)`
    
2. **Binary Search:** `O(log K)`
    
3. **Total Complexity:** **`O(log K)`**, where `K` is the target index.
    

---

## **🔹 Summary**

- Use **exponential search** to determine an appropriate range.
    
- Perform **binary search** in the discovered range.
    
- **Optimized for large/infinite sorted arrays** without needing `arr.length`.
    

🚀 **Best approach for unknown-sized sorted arrays!**