# **🔍 Search a 2D Matrix II – Full Notes**

## **📌 Problem Statement (Leetcode 240 – Search a 2D Matrix II)**

You are given an `m x n` **sorted 2D matrix**, where:

1. **Each row** is sorted **in increasing order** from left to right.
    
2. **Each column** is sorted **in increasing order** from top to bottom.
    

Write an algorithm to search for a given `target` value in the matrix. Return `true` if the target exists and `false` otherwise.

---

## **💡 Key Observations**

Unlike **Leetcode 74**, where the matrix is **sorted row-wise globally**, this matrix follows a **2D sorted property**:

- **Smaller values are on the left & top**.
    
- **Larger values are on the right & bottom**.
    

This structure allows us to efficiently **eliminate** rows or columns in each step.

---

## **🛠️ Steps to Solve Using the "Staircase Search" Approach**

1. **Start from the top-right corner** (`matrix[0][n-1]`):
    
    - If `matrix[row][col] == target`, return `true`.
        
    - If `matrix[row][col] > target`, move **left** (eliminate the current column).
        
    - If `matrix[row][col] < target`, move **down** (eliminate the current row).
        
2. Continue this process until:
    
    - The indices go out of bounds (`row >= m` or `col < 0`).
        
    - The target is found.
        

---

## **⏳ Time Complexity Analysis**

- **At each step**, we either **move left** (reduce `n` by 1) or **move down** (reduce `m` by 1).
    
- The worst-case scenario takes `O(m + n)` steps, where we traverse the entire matrix diagonally.
    
- **Best Case:** `O(1)` (if the target is at the starting point).
    
- **Average Case:** `O(m + n)`.
    
- **Space Complexity:** `O(1)` (no extra space used).
    

---

## **📌 Java Solution (Staircase Search)**

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return false;
        }

        int m = matrix.length, n = matrix[0].length;
        int row = 0, col = n - 1; // Start from the top-right corner

        while (row < m && col >= 0) {
            if (matrix[row][col] == target) {
                return true; // Found target
            } else if (matrix[row][col] > target) {
                col--; // Move left
            } else {
                row++; // Move down
            }
        }
        return false; // Target not found
    }
}
```

---

## **📌 Example Walkthrough**

### **Example 1**

```
matrix = [
  [1,  4,  7,  11],
  [2,  5,  8,  12],
  [3,  6,  9,  16],
  [10, 13, 14, 17]
]
target = 5
```

🔹 **Starting at `matrix[0][3] = 11`**

|Step|Position (`row, col`)|Value|Action|
|---|---|---|---|
|1|`(0,3)`|`11`|`11 > 5` → Move left to `(0,2)`|
|2|`(0,2)`|`7`|`7 > 5` → Move left to `(0,1)`|
|3|`(0,1)`|`4`|`4 < 5` → Move down to `(1,1)`|
|4|`(1,1)`|`5`|✅ Found target → Return `true`|

---

## **📌 Edge Cases to Consider**

1. **Empty matrix** → Return `false`.
    
2. **Single row/single column matrix** → Should still work.
    
3. **Target smaller than the smallest or larger than the largest element** → Return `false`.
    
4. **Target at first or last index** → Should return `true`.
    

---

## **🔹 Alternative Approach – Binary Search on Each Row**

Instead of **staircase search**, we can:

1. **Iterate over each row** and apply **binary search** in that row.
    
2. **Binary search time complexity per row** = `O(log n)`, so the total time complexity is `O(m log n)`.
    

🔸 **Time Complexity:** `O(m log n)`, better when `m >> n` but slower than `O(m + n)` in general.  
🔹 **Not preferred over Staircase Search due to higher worst-case complexity**.

---

## **📝 Summary Table**

|**Approach**|**Time Complexity**|**Space Complexity**|**Best Used When?**|
|---|---|---|---|
|**Staircase Search**|`O(m + n)`|`O(1)`|Most efficient for Leetcode 240|
|**Binary Search per Row**|`O(m log n)`|`O(1)`|If `m` is very large compared to `n`|

---

## **🔍 Related Problems**

1. **Leetcode 74 – Search a 2D Matrix** (Globally row-wise sorted)
    
2. **Leetcode 378 – Kth Smallest Element in a Sorted Matrix**
    
3. **Leetcode 668 – Kth Smallest Number in Multiplication Table**
    

This concludes the **detailed revision notes** for **Search in a 2D Matrix II**. 🚀