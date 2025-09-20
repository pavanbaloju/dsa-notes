# **📌 Kth Smallest Element in a Sorted Matrix (Binary Search Approach) – Final Notes**

## **🔹 Problem Statement**

Given an **N × N** matrix where **each row and each column is sorted in ascending order**, find the **k-th smallest element**.

---

## **💡 Approach – Binary Search on Answer**

Since the **matrix is sorted row-wise and column-wise**, we don’t need to sort all elements explicitly. Instead, we apply **Binary Search on Answer**.

### **1️⃣ Define Search Space**

- **Minimum possible value:** `low = matrix[0][0]` (smallest element in matrix).
    
- **Maximum possible value:** `high = matrix[N-1][N-1]` (largest element in matrix).
    

### **2️⃣ Apply Binary Search**

- **Midpoint (`mid`)** represents a possible candidate for the k-th smallest element.
    
- Use `countLessEqual(matrix, mid)` to count elements **≤ mid**.
    
- If `count >= k`, search in the **lower half** (`high = mid`).
    
- Otherwise, search in the **upper half** (`low = mid + 1`).
    

---

## **🔹 `countLessEqual(matrix, mid)` – Key Function**

To count elements **≤ mid** efficiently, use **greedy traversal** from the **bottom-left**:

1. **Start at `matrix[N-1][0]`** (bottom-left corner).
    
2. If `matrix[row][col] ≤ mid`, **add (row + 1) to count** (all elements in column ≤ mid), move **right**.
    
3. If `matrix[row][col] > mid`, move **up**.
    
4. Stop when out of bounds.
    

⏳ **Time Complexity:** `O(N)`

---

## **🔹 Final Java Code**

```java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int n = matrix.length;
        int low = matrix[0][0], high = matrix[n - 1][n - 1];

        while (low < high) {
            int mid = low + (high - low) / 2;
            if (countLessEqual(matrix, mid) >= k) {
                high = mid; // Search left half
            } else {
                low = mid + 1; // Search right half
            }
        }
        return low;
    }

    private int countLessEqual(int[][] matrix, int mid) {
        int n = matrix.length, count = 0;
        int row = n - 1, col = 0;

        while (row >= 0 && col < n) {
            if (matrix[row][col] <= mid) {
                count += (row + 1);
                col++;
            } else {
                row--;
            }
        }
        return count;
    }
}
```

---

## **🔹 Complexity Analysis**

- **Binary Search on Answer**: `O(log(max-min))`
    
- **Counting elements using `countLessEqual`**: `O(N)`
    
- **Overall Complexity**: **O(N log(max-min))**
    

---

## **🔹 Why Binary Search Works Here?**

✅ **Sorted Property** → Helps define a numerical range `[min, max]`.  
✅ **Counting elements efficiently** → Using `countLessEqual(matrix, mid)`.  
✅ **Binary search ensures k-th smallest is found optimally**.

This approach is **faster** than **min-heap (O(N² log k))** and **brute-force sorting (O(N² log N²))**.

---

## **🔹 Example Walkthrough**

### **Input**

```java
matrix = [
    [1,  5,  9],
    [10, 11, 13],
    [12, 13, 15]
]
k = 8
```

### **Binary Search Steps**

|Iteration|`low`|`high`|`mid`|`countLessEqual(matrix, mid)`|Action|
|---|---|---|---|---|---|
|1|1|15|8|4|`low = mid + 1`|
|2|9|15|12|6|`low = mid + 1`|
|3|13|15|13|8|`high = mid`|
|4|13|13|-|-|Found `13`|

**✅ Output:** `13`

---

## **🔹 Summary**

|**Step**|**Details**|
|---|---|
|**Step 1**|Use **Binary Search on Answer** within `[matrix[0][0], matrix[N-1][N-1]]`|
|**Step 2**|Use `countLessEqual(matrix, mid)` to check how many elements ≤ `mid`|
|**Step 3**|If `count >= k`, reduce `high`; else increase `low`|
|**Step 4**|Return `low` when search space is exhausted|

🔥 **Optimal and efficient approach for searching in sorted matrices!** 🚀