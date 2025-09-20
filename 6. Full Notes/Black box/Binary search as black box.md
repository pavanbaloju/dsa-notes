Here’s the **Black Box Learning Breakdown for Binary Search**, including **Java examples** and a structured approach.

---

# **Binary Search – Black Box Learning Approach**

## **1. Input**

Binary Search works on a **sorted array** and efficiently finds a **target value**.

- **Input:** A **sorted** array and a target element.
- **Condition:** Elements must be in increasing or decreasing order.

### **Example Input in Java**

```java
int[] arr = {2, 5, 8, 12, 16, 23};
int target = 8;
```

---

## **2. Output**

- **Index of the target element** if found.
- **-1** if the target element is not present in the array.

Example Output:

```java
System.out.println(binarySearch(arr, target));  // Output: 2 (index of 8)
```

---

## **3. Operations**

### **Basic Operations**

|Operation|Example (Java)|Best Case|Average Case|Worst Case|Space Complexity|
|---|---|---|---|---|---|
|**Search in Sorted Array**|`binarySearch(arr, x);`|**O(1)**|**O(log n)**|**O(log n)**|**O(1)**|
|**Search in Rotated Array**|`searchRotated(arr, x);`|**O(1)**|**O(log n)**|**O(log n)**|**O(1)**|
|**Find First Occurrence**|`firstOccurrence(arr, x);`|**O(1)**|**O(log n)**|**O(log n)**|**O(1)**|
|**Find Last Occurrence**|`lastOccurrence(arr, x);`|**O(1)**|**O(log n)**|**O(log n)**|**O(1)**|
|**Find Element in Infinite Array**|`searchInfinite(arr, x);`|**O(1)**|**O(log n)**|**O(log n)**|**O(1)**|

---

## **4. Time and Space Complexities**

### **Time Complexity Summary**

|Operation|Best Case|Average Case|Worst Case|
|---|---|---|---|
|**Standard Binary Search**|O(1)|O(log n)|O(log n)|
|**Search in Rotated Array**|O(1)|O(log n)|O(log n)|
|**Find First/Last Occurrence**|O(1)|O(log n)|O(log n)|

### **Space Complexity**

- **O(1)** for iterative implementation.
- **O(log n)** for recursive implementation (due to recursive call stack).

---

## **5. Use Cases (Problem Patterns)**

- **Element Searching in Sorted Arrays:** Find an element in a sorted list.
- **Finding First/Last Occurrence of an Element:** Locate duplicate elements efficiently.
- **Searching in Rotated Sorted Arrays:** Find an element when the array is cyclically shifted.
- **Finding Peak Element in an Array:** Locate an element greater than neighbors.
- **Finding Square Root or K-th Root:** Use binary search instead of brute force.

---

## **6. Problems in this Pattern**

### **Easy**

- Find an Element in a Sorted Array
- First and Last Occurrence of an Element
- Find Square Root of a Number (Using Binary Search)

### **Medium**

- Search in a Rotated Sorted Array
- Find Peak Element in an Array
- Find the Minimum in a Rotated Sorted Array

### **Hard**

- Median of Two Sorted Arrays
- Find Kth Smallest Element in Two Sorted Arrays
- Find the Missing Number in a Consecutive Sequence

---

## **7. Explore - Other Related Concepts**

- **Ternary Search:** Similar to binary search but splits into three parts.
- **Exponential Search:** Used for searching in infinite arrays.
- **Fibonacci Search:** An alternative search technique for sorted arrays.
- **Interpolation Search:** Works better when data is uniformly distributed.
- **Binary Search on Answer:** Used in problems like "Find the Maximum Minimum Distance".

---

## **8. Code Implementation**

### **Iterative Binary Search**

```java
class BinarySearch {
    static int binarySearch(int[] arr, int target) {
        int left = 0, right = arr.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (arr[mid] == target) return mid;
            if (arr[mid] < target) left = mid + 1;
            else right = mid - 1;
        }
        return -1;
    }

    public static void main(String[] args) {
        int[] arr = {2, 5, 8, 12, 16, 23};
        System.out.println(binarySearch(arr, 8));  // Output: 2
    }
}
```

### **Recursive Binary Search**

```java
class BinarySearchRecursive {
    static int binarySearch(int[] arr, int left, int right, int target) {
        if (left > right) return -1;
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) return mid;
        return arr[mid] < target
            ? binarySearch(arr, mid + 1, right, target)
            : binarySearch(arr, left, mid - 1, target);
    }

    public static void main(String[] args) {
        int[] arr = {2, 5, 8, 12, 16, 23};
        System.out.println(binarySearch(arr, 0, arr.length - 1, 8));  // Output: 2
    }
}
```

---

## **Conclusion**

By treating **Binary Search as a black box**, we:  
✅ **Observed how input changes affect output.**  
✅ **Identified patterns in operations.**  
✅ **Implemented solutions before diving into deep theory.**

Would you like to continue with **Binary Search on Answer (Advanced Applications) or Ternary Search next?**