Here’s the **Black Box Learning Breakdown for Recursion**, including **Java examples** and a structured approach.

---

# **Recursion – Black Box Learning Approach**

## **1. Input**

Recursion is a technique where a function **calls itself** to solve a problem.

- **Base Case:** Defines the stopping condition to prevent infinite recursion.
- **Recursive Case:** Breaks the problem into smaller subproblems.

### **Example Input in Java (Factorial Calculation)**

```java
int n = 5;
```

---

## **2. Output**

- **A solution built by breaking the problem into smaller subproblems.**
- **Recursive function eventually returns a final result.**

Example Output:

```java
System.out.println(factorial(n)); // Output: 120
```

---

## **3. Operations (Recursive Techniques Ranked by Complexity)**

|Recursion Type|Example (Java)|Best Case|Average Case|Worst Case|Space Complexity|
|---|---|---|---|---|---|
|**Simple Recursion**|`factorial(n);`|**O(1)**|**O(n)**|**O(n)**|**O(n) (call stack)**|
|**Tail Recursion**|`tailFactorial(n, acc);`|**O(1)**|**O(n)**|**O(n)**|**O(1) (if optimized)**|
|**Tree Recursion**|`fibonacci(n);`|**O(1)**|**O(2ⁿ)**|**O(2ⁿ)**|**O(n)**|
|**Backtracking**|`solveMaze(x, y);`|**O(1)**|**O(2ⁿ)**|**O(2ⁿ)**|**O(n) (stack depth)**|
|**Dynamic Programming (Memoization)**|`fibonacciMemo(n, memo);`|**O(1)**|**O(n)**|**O(n)**|**O(n)**|
|**Divide and Conquer**|`mergeSort(arr, l, r);`|**O(n log n)**|**O(n log n)**|**O(n log n)**|**O(log n)**|

---

## **4. Time and Space Complexities**

### **Time Complexity Summary**

|Type of Recursion|Best Case|Average Case|Worst Case|
|---|---|---|---|
|**Simple Recursion (Factorial, Sum of Digits)**|O(1)|O(n)|O(n)|
|**Tail Recursion (Optimized Factorial)**|O(1)|O(n)|O(n)|
|**Tree Recursion (Fibonacci, Exponential Growth)**|O(1)|O(2ⁿ)|O(2ⁿ)|
|**Backtracking (Maze, N-Queens, Subsets)**|O(1)|O(2ⁿ)|O(2ⁿ)|
|**Memoized Recursion (Optimized Fibonacci, DP Problems)**|O(1)|O(n)|O(n)|
|**Divide & Conquer (Merge Sort, Quick Sort)**|O(n log n)|O(n log n)|O(n log n)|

### **Space Complexity**

- **O(n)** for normal recursive calls due to the function call stack.
- **O(1)** for **tail recursion** (if optimized by the compiler).
- **O(log n)** for **divide and conquer** algorithms like Merge Sort.

---

## **5. Use Cases (Problem Patterns)**

- **Mathematical Computations:** Factorial, Fibonacci, Exponentiation.
- **Tree & Graph Traversal:** DFS, Preorder, Inorder, Postorder.
- **Divide and Conquer Algorithms:** Merge Sort, Quick Sort, Binary Search.
- **Backtracking Problems:** N-Queens, Sudoku Solver, Subsets Generation.
- **Dynamic Programming:** Recursive Fibonacci with memoization.

---

## **6. Problems in this Pattern**

### **Easy**

- Compute Factorial Using Recursion
- Find Nth Fibonacci Number (Recursive)
- Sum of Digits of a Number

### **Medium**

- Generate All Subsets of an Array (Backtracking)
- Merge Sort (Divide & Conquer)
- Recursive Binary Search

### **Hard**

- N-Queens Problem (Backtracking)
- Word Search in a Grid (Backtracking)
- Longest Common Subsequence (Recursive DP)

---

## **7. Explore - Other Related Concepts**

- **Tail Recursion Optimization:** Reduces memory usage.
- **Dynamic Programming (Memoization vs. Tabulation):** Optimizes recursive solutions.
- **Backtracking with Pruning:** Reduces the number of recursive calls.
- **Recursive Graph Traversal:** DFS for connected components.
- **Recursion vs. Iteration:** Trade-offs between readability and performance.

---

## **8. Code Implementations**

### **Factorial Using Recursion**

```java
class RecursionExamples {
    static int factorial(int n) {
        if (n == 0) return 1; // Base case
        return n * factorial(n - 1); // Recursive case
    }

    public static void main(String[] args) {
        System.out.println(factorial(5));  // Output: 120
    }
}
```

### **Fibonacci Using Recursion**

```java
class FibonacciRecursion {
    static int fibonacci(int n) {
        if (n <= 1) return n; // Base cases
        return fibonacci(n - 1) + fibonacci(n - 2); // Recursive case
    }

    public static void main(String[] args) {
        System.out.println(fibonacci(5));  // Output: 5
    }
}
```

### **Merge Sort Using Recursion**

```java
class MergeSort {
    static void mergeSort(int[] arr, int left, int right) {
        if (left < right) {
            int mid = left + (right - left) / 2;
            mergeSort(arr, left, mid);
            mergeSort(arr, mid + 1, right);
            merge(arr, left, mid, right);
        }
    }

    static void merge(int[] arr, int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;
        int[] leftArr = new int[n1];
        int[] rightArr = new int[n2];

        for (int i = 0; i < n1; i++) leftArr[i] = arr[left + i];
        for (int i = 0; i < n2; i++) rightArr[i] = arr[mid + 1 + i];

        int i = 0, j = 0, k = left;
        while (i < n1 && j < n2) {
            arr[k++] = (leftArr[i] <= rightArr[j]) ? leftArr[i++] : rightArr[j++];
        }
        while (i < n1) arr[k++] = leftArr[i++];
        while (j < n2) arr[k++] = rightArr[j++];
    }

    public static void main(String[] args) {
        int[] arr = {5, 2, 8, 1, 6};
        mergeSort(arr, 0, arr.length - 1);
        System.out.println(Arrays.toString(arr)); // Output: [1, 2, 5, 6, 8]
    }
}
```

---

## **Conclusion**

By treating Recursion as a **black box**, we:  
✅ **Observed how input changes affect output.**  
✅ **Identified patterns in operations.**  
✅ **Implemented solutions before diving into deep theory.**

Would you like to continue with **Backtracking (Advanced Recursion) or Dynamic Programming next?**