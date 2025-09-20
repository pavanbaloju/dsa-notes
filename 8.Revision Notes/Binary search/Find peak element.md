# **Find Peak Element – Full Notes**

## **🔹 Problem Statement**

Given an integer array `nums`, find a **peak element** and return its index.  
A **peak element** is an element that is **strictly greater than its neighbors**.

- You may assume `nums[-1] = -∞` and `nums[n] = -∞`, meaning the boundaries are always smaller than any valid element.
    
- If multiple peaks exist, return **any** peak index.
    
- The array does **not** have to be sorted.
    

📌 **Example 1:**  
**Input:** `nums = [1,2,3,1]`  
**Output:** `2` (Index of `3` is a peak)

📌 **Example 2:**  
**Input:** `nums = [1,2,1,3,5,6,4]`  
**Output:** `1` or `5` (Index of `2` or `6` are peaks)

---

## **🔹 Intuition Behind the Problem**

1. A peak element is greater than its neighbors.
    
2. If an element is **less than the next element (`nums[mid] < nums[mid+1]`)**, a peak must exist on the **right side**.
    
3. If an element is **greater than the next element (`nums[mid] > nums[mid+1]`)**, a peak must exist on the **left side** (or the current element itself is a peak).
    
4. The problem guarantees **at least one peak** due to the `-∞` boundary.
    

---

## **🔹 Approaches**

### **1️⃣ Linear Scan (Brute Force) – O(N)**

- Check each element and see if it is greater than its neighbors.
    
- **Time Complexity:** `O(N)`
    
- **Space Complexity:** `O(1)`
    

```java
public int findPeakElement(int[] nums) {
    int n = nums.length;
    for (int i = 0; i < n - 1; i++) {
        if (nums[i] > nums[i + 1]) return i;
    }
    return n - 1;  // Last element is the peak if no earlier peak found
}
```

✅ **Easy to implement but inefficient for large arrays.**

---

### **2️⃣ Binary Search (Optimized) – O(log N)**

**Key Idea:**

- Instead of scanning **every** element, we divide the search space.
    
- **If `nums[mid] < nums[mid + 1]`, the peak is on the right side** (move `low = mid + 1`).
    
- **If `nums[mid] > nums[mid + 1]`, the peak is on the left side** (move `high = mid`).
    

#### **Code:**

```java
public int findPeakElement(int[] nums) {
    int low = 0, high = nums.length - 1;
    
    while (low < high) {  // Use while(low < high)
        int mid = low + (high - low) / 2;

        if (nums[mid] > nums[mid + 1]) {
            high = mid;  // Search left half
        } else {
            low = mid + 1;  // Search right half
        }
    }
    return low;  // At the end, low == high, which is the peak index
}
```

**🧐 Why `low < high` instead of `low <= high`?**

- Since we always compare `mid` with `mid + 1`, there is **no need to check when `low == high`**.
    
- The search space **naturally shrinks** until `low == high`, which is our peak.
    

---

## **🔹 Dry Run Example**

🔹 **Example:** `nums = [1, 2, 1, 3, 5, 6, 4]`

```
Iteration 1: low = 0, high = 6, mid = 3 → nums[3] = 3 < nums[4] = 5 → move right (low = 4)
Iteration 2: low = 4, high = 6, mid = 5 → nums[5] = 6 > nums[6] = 4 → move left (high = 5)
Iteration 3: low = 4, high = 5, mid = 4 → nums[4] = 5 < nums[5] = 6 → move right (low = 5)
End: low == high, return index 5 (peak at `nums[5] = 6`)
```

---

## **🔹 Complexity Analysis**

|**Approach**|**Time Complexity**|**Space Complexity**|**Why?**|
|---|---|---|---|
|Brute Force (Linear Scan)|`O(N)`|`O(1)`|Checks each element|
|Binary Search|`O(log N)`|`O(1)`|Cuts search space in half|

✅ **Binary Search is optimal and guarantees a peak in `O(log N)`.**

---

## **🔹 Edge Cases to Consider**

1️⃣ **Single Element:** `nums = [3]` → Peak is `3` at index `0`.  
2️⃣ **Strictly Increasing Array:** `nums = [1,2,3,4,5]` → Last element is the peak.  
3️⃣ **Strictly Decreasing Array:** `nums = [5,4,3,2,1]` → First element is the peak.  
4️⃣ **Multiple Peaks:** `nums = [1,2,1,3,5,6,4]` → Multiple valid answers (`1` or `5`).

---

## **🔹 Summary**

- **Problem Type:** Find a peak in an **unsorted** array.
    
- **Key Idea:** Use **binary search** by comparing `nums[mid]` with `nums[mid+1]`.
    
- **Best Approach:** `O(log N)` **Binary Search**, reducing search space intelligently.
    
- **Multiple Solutions:** Any peak is a valid answer.
    

✅ **This problem is a great introduction to Binary Search on Unsorted Arrays!**