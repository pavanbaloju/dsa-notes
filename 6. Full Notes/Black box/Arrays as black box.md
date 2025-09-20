# **Arrays – Black Box Learning Approach**

## **1. Input**

- **Fixed size** (static arrays in Java).
- **Homogeneous data type** (all elements must be of the same type).
- **Indexed access** (zero-based indexing).

Example in Java:

```java
int[] arr1 = {1, 2, 3, 4, 5};  // Static array
int[] arr2 = new int[5];  // Array of size 5 with default values (0)
```

---

## **2. Output**

- **Element at a given index** (`arr[i]`).
- **A modified version** after insertions, deletions, or sorting.
- **Subarrays** (by manually copying elements).

Example:

```java
System.out.println(arr1[2]);  // Output: 3
```

---

## **3. Operations**

### **Basic Operations**

|Operation|Example (Java)|Time Complexity|
|---|---|---|
|**Access**|`arr[i]`|**O(1)**|
|**Modify**|`arr[i] = newValue;`|**O(1)**|
|**Insert at End (ArrayList)**|`list.add(x);`|**O(1) amortized**|
|**Insert at Start/Middle**|`System.arraycopy()`|**O(n)**|
|**Delete at End (ArrayList)**|`list.remove(list.size() - 1);`|**O(1)**|
|**Delete at Start/Middle**|`System.arraycopy()`|**O(n)**|
|**Linear Search**|`for (int x : arr) if(x == target) return true;`|**O(n)**|
|**Binary Search (Sorted Array)**|`Arrays.binarySearch(arr, x);`|**O(log n)**|
|**Sorting**|`Arrays.sort(arr);`|**O(n log n)**|

---

## **4. Time and Space Complexities**

### **Time Complexity Summary**

|Operation|Best Case|Worst Case|
|---|---|---|
|**Index Access**|O(1)|O(1)|
|**Insertion (End, Dynamic ArrayList)**|O(1)|O(n) (resizing required)|
|**Insertion (Middle/Start, Static Array)**|O(n)|O(n)|
|**Deletion (End, ArrayList)**|O(1)|O(n) (if shifting required)|
|**Sorting**|O(n log n)|O(n log n)|
|**Searching (Linear)**|O(1)|O(n)|
|**Searching (Binary, Sorted Array)**|O(1)|O(log n)|

### **Space Complexity**

- **O(n)** for storing elements.
- **O(1)** extra space if modifying in place.

---

## **5. Use Cases**

- **Index-based access** (e.g., Lookup tables).
- **Efficient traversal** (e.g., Sliding Window problems).
- **Sorting & Searching** (e.g., Binary search on sorted arrays).
- **Mathematical computations** (e.g., Prefix sum).

---

## **6. Problems in this Pattern**

### **Easy**

- Find Maximum/Minimum in an Array
- Reverse an Array
- Check if an Array is Sorted

### **Medium**

- Find Kth Largest Element
- Two Sum Problem
- Rotate an Array

### **Hard**

- Maximum Subarray Sum (Kadane’s Algorithm)
- Merge Intervals
- Trapping Rain Water

---

## **7. Explore - Other Related Concepts**

- **Linked Lists**: Better for insertions/deletions.
- **HashMaps**: Faster lookup than arrays in some cases.
- **Stacks/Queues**: Specialized structures built on arrays.
- **Prefix Sum / Difference Arrays**: Optimized range queries.
- **Binary Search**: Fast searching on sorted arrays.

---



