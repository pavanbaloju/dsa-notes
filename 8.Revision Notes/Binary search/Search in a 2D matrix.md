## **🔍 Search in a 2D Matrix – Full Notes**

### **📌 Problem Statement (Leetcode 74 – Search a 2D Matrix)**

Given an `m x n` matrix where:

1. Each **row** is sorted from left to right.
    
2. The **first element** of each row is **greater than** the last element of the previous row.
    

Write an algorithm to search for a given `target` value in the matrix. Return `true` if the target exists and `false` otherwise.

---

## **💡 Key Observations**

1. The matrix can be **flattened** into a **sorted 1D array** without actually transforming it.
    
2. **Binary Search** can be applied directly since the elements are **sorted in increasing order** when read row-wise.
    
3. A **virtual index mapping** is needed to map 1D indices back to the **2D matrix**.
    

---

## **🛠️ Steps to Solve**

1. Consider the matrix as a **1D sorted array** of length `m * n`.
    
2. Apply **binary search** with:
    
    - `low = 0`, `high = (m * n) - 1`.
        
    - Compute `mid = (low + high) / 2` to find the middle index in this **virtual 1D array**.
        
    - Convert the `mid` index into **matrix row & column** using:
        
        ```
        row = mid / n
        col = mid % n
        ```
        
    - Compare `matrix[row][col]` with `target`:
        
        - If **equal**, return `true`.
            
        - If **smaller**, search the **right half** (`low = mid + 1`).
            
        - If **greater**, search the **left half** (`high = mid - 1`).
            
3. If the loop ends without finding the target, return `false`.
    

---

## **⏳ Time Complexity Analysis**

- **Binary Search on `m * n` elements** → `O(log(m * n))`.
    
- **Space Complexity** → `O(1)` (No extra space used).
    

---

## **📌 Java Solution (Binary Search)**

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return false;
        }

        int m = matrix.length, n = matrix[0].length;
        int low = 0, high = m * n - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;
            int row = mid / n;
            int col = mid % n;

            if (matrix[row][col] == target) {
                return true;
            } else if (matrix[row][col] < target) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        return false;
    }
}
```

---

## **📌 Example Walkthrough**

### **Example 1**

```
matrix = [
  [1,  3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 60]
]
target = 3
```

🔹 **Matrix as 1D Array Representation:**  
`[1, 3, 5, 7, 10, 11, 16, 20, 23, 30, 34, 60]`

|Iteration|`mid`|`row`|`col`|`matrix[row][col]`|Action|
|---|---|---|---|---|---|
|1st|5|1|1|`matrix[1][1] = 11`|`11 > 3`, search left (`high = 4`)|
|2nd|2|0|2|`matrix[0][2] = 5`|`5 > 3`, search left (`high = 1`)|
|3rd|0|0|0|`matrix[0][0] = 1`|`1 < 3`, search right (`low = 1`)|
|4th|1|0|1|`matrix[0][1] = 3`|✅ **Found target**|

---

## **📌 Edge Cases to Consider**

1. **Empty matrix** → Return `false`.
    
2. **Single row/single column matrix** → Should still work.
    
3. **Target smaller than smallest or larger than largest element** → Return `false`.
    
4. **Target at first or last index** → Should return `true`.
    

---

## **🔹 Alternative Approach – Row-Wise Binary Search**

Instead of treating the matrix as a **1D array**, we can:

1. **Find the correct row** using binary search on the first column.
    
2. **Perform another binary search** in that row.
    

🔸 **Time Complexity:** `O(log m + log n) = O(log(m * n))`  
🔹 **Not preferred over the 1D binary search method as it has the same time complexity but more steps.**

---

## **📝 Summary Table**

|**Approach**|**Time Complexity**|**Space Complexity**|**Best Used When?**|
|---|---|---|---|
|**1D Binary Search (Virtual Indexing)**|`O(log(m * n))`|`O(1)`|Most efficient for Leetcode 74|
|**Row-wise Binary Search**|`O(log m + log n)`|`O(1)`|When a direct binary search isn't possible|

---

## **🔍 Related Problems**

1. **Leetcode 240 – Search a 2D Matrix II** (Sorted row-wise and column-wise)
    
2. **Leetcode 378 – Kth Smallest Element in a Sorted Matrix**
    
3. **Leetcode 668 – Kth Smallest Number in Multiplication Table**
    

This concludes the **detailed revision notes** for **Search in a 2D Matrix**. 🚀