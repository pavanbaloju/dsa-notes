# **🗻 Peak Index in Mountain Array – Full Notes**

## **🔹 Problem Statement**

A **mountain array** is an array that:

1. **Strictly increases** to a peak element.
    
2. **Strictly decreases** after the peak.
    

Given such an array, **find the index of the peak element** (largest element).

📌 **Example 1:**  
**Input:** `arr = [0,1,2,3,5,3,1]`  
**Output:** `4` (Peak at index `4`, `arr[4] = 5`)

📌 **Example 2:**  
**Input:** `arr = [3,5,3,2,0]`  
**Output:** `1` (Peak at index `1`, `arr[1] = 5`)

---

## **🔹 Observations**

1. **One peak exists** since it is a valid mountain array.
    
2. If `arr[mid] < arr[mid + 1]`, then the peak is **on the right**.
    
3. If `arr[mid] > arr[mid + 1]`, then the peak is **on the left** (or `mid` itself is the peak).
    

---

## **🔹 Approaches**

### **1️⃣ Brute Force – O(N)**

Loop through the array and return the index of the **largest element**.

**Code:**

```java
public int peakIndexInMountainArray(int[] arr) {
    for (int i = 1; i < arr.length - 1; i++) {
        if (arr[i] > arr[i + 1]) return i;
    }
    return -1; // This should never be reached in a valid mountain array.
}
```

**✅ Simple but inefficient (`O(N)`).**

---

### **2️⃣ Optimized Approach – Binary Search (O(log N))**

**Key Idea:**

- Use **binary search** to locate the peak efficiently.
    
- If `arr[mid] < arr[mid + 1]`, move **right** (peak is ahead).
    
- If `arr[mid] > arr[mid + 1]`, move **left** (or `mid` itself is the peak).
    

---

### **🔹 Binary Search Code (O(log N))**

```java
public int peakIndexInMountainArray(int[] arr) {
    int low = 0, high = arr.length - 1;

    while (low < high) {  // Use while(low < high)
        int mid = low + (high - low) / 2;

        if (arr[mid] < arr[mid + 1]) {
            low = mid + 1;  // Move right
        } else {
            high = mid;  // Move left
        }
    }
    return low;  // `low == high`, which is the peak index
}
```

---

## **🔹 Dry Run Example**

🔹 **Example:** `arr = [0,1,2,3,5,3,1]`

```
Iteration 1: low = 0, high = 6, mid = 3 → arr[3] = 3 < arr[4] = 5 → move right (low = 4)
Iteration 2: low = 4, high = 6, mid = 5 → arr[5] = 3 > arr[6] = 1 → move left (high = 5)
Iteration 3: low = 4, high = 5, mid = 4 → arr[4] = 5 > arr[5] = 3 → move left (high = 4)
End: low == high, return index 4 (peak at `arr[4] = 5`)
```

---

## **🔹 Complexity Analysis**

|**Approach**|**Time Complexity**|**Space Complexity**|**Why?**|
|---|---|---|---|
|Brute Force (Linear Scan)|`O(N)`|`O(1)`|Scans all elements|
|Binary Search|`O(log N)`|`O(1)`|Reduces search space efficiently|

✅ **Binary Search is optimal and guarantees a peak in `O(log N)`.**

---

## **🔹 Edge Cases to Consider**

1️⃣ **Minimum Length Mountain:** `arr = [1,2,1]` → Peak is `2` at index `1`.  
2️⃣ **Long Increasing Sequence:** `arr = [1,2,3,4,5,6,7,8,9,6,2]` → Peak at `8` (index `8`).  
3️⃣ **Long Decreasing Sequence:** `arr = [3,5,8,12,15,20,17,10,5,1]` → Peak at `20` (index `5`).

---

## **🔹 Summary**

- **Problem Type:** Find the peak in a **mountain array**.
    
- **Key Idea:** Use **binary search** by comparing `arr[mid]` with `arr[mid+1]`.
    
- **Best Approach:** `O(log N)` **Binary Search**, reducing search space intelligently.
    
- **Guaranteed Peak:** The problem guarantees **exactly one peak**.
    

✅ **This problem is an application of the "Find Peak Element" pattern.**