# **Kth Largest in a Sorted Matrix – Binary Search Approach**

## **🔹 Problem Statement**

Given an `n x n` matrix where each row and column is sorted in ascending order, find the **k-th largest** element.

## **🔹 Key Idea: Binary Search on Answer**

- Instead of searching for an index, we **search for a numerical answer**.
    
- The answer lies **between the smallest and largest element** in the matrix.
    
- Use **binary search on this range** to efficiently find the k-th largest element.
    

---

## **🔹 Approach**

1. **Define Binary Search Range:**
    
    - `low = matrix[0][0]` (smallest element in matrix).
        
    - `high = matrix[n-1][n-1]` (largest element in matrix).
        
2. **Binary Search Condition:**
    
    - Find `mid = (low + high) / 2`
        
    - Count how many elements in the matrix are **greater than or equal to `mid`**.
        
    - If count **≥ k**, move search right (`low = mid + 1`).
        
    - Otherwise, move search left (`high = mid`).
        
3. **Efficiently Counting Elements ≥ `mid`**
    
    - Start from the **top-right corner**.
        
    - If `matrix[row][col] ≥ mid`, all elements below it are also **≥ mid**, so add `(n - col)` to count.
        
    - Otherwise, move left.
        
4. **Return `high`**
    
    - `low` and `high` converge, and `high` stores the k-th largest element.
        

---

## **🔹 Code Implementation (Java)**

```java
class Solution {
    public int kthLargest(int[][] matrix, int k) {
        int n = matrix.length;
        
        // Define the search space
        int low = matrix[0][0];
        int high = matrix[n - 1][n - 1];

        while (low < high) {
            int mid = low + (high - low) / 2;

            if (countGreaterEqual(matrix, mid) >= k) {
                low = mid + 1; // Search right
            } else {
                high = mid; // Search left
            }
        }
        return high;
    }

    // Helper function to count elements >= mid
    private int countGreaterEqual(int[][] matrix, int mid) {
        int n = matrix.length, count = 0;
        int row = 0, col = n - 1;

        while (row < n && col >= 0) {
            if (matrix[row][col] >= mid) {
                count += (n - col);
                row++; // Move downward
            } else {
                col--; // Move left
            }
        }
        return count;
    }
}
```

---

## **🔹 Why Binary Search Works?**

✅ **Matrix is sorted** → We can efficiently count elements ≥ `mid`.  
✅ **Binary search halves the search space** → `O(N log(max-min))` complexity.

---

## **🔹 Time Complexity Analysis**

1. **Binary Search Range:** `O(log(max-min))`
    
2. **Counting Elements:** `O(N)`
    
3. **Total Complexity:** **`O(N log(max-min))`**
    

🚀 **Efficient and optimal approach for k-th largest in a sorted matrix!**