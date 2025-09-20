

## **1️⃣ Standard Binary Search (Exact Match)**

- **Problem Type:** Search for an element in a sorted array.
- **Key Idea:** Repeatedly divide the array in half until the target is found.
- **Examples:**
    - **Leetcode 704 – Binary Search** (Find target in sorted array)
    - **Leetcode 278 – First Bad Version** (Find first occurrence of `true` in a sorted boolean array)

1. [[Binary search to find a number in sorted array]]
2. [[First bad version]]
3. [[Search insert position]]

---

## **2️⃣ Finding First or Last Occurrence (Lower & Upper Bound)**

- **Problem Type:** Find the **first** or **last occurrence** of an element in a sorted array.
- **Key Idea:** Modify standard binary search to track positions.
- **Examples:**
    - **Leetcode 34 – Find First and Last Position of Element in Sorted Array** (Lower and Upper Bound)
    - **Leetcode 852 – Peak Index in a Mountain Array** (Find peak element)
1. [[Lower bound]]
2. [[Upper bound]]

---

## **3️⃣ Search in Rotated or Modified Arrays**

- **Problem Type:** Search in a sorted but **rotated** or **nearly sorted** array.
- **Key Idea:** Identify the rotation point and apply binary search accordingly.
- **Examples:**
    - **Leetcode 33 – Search in Rotated Sorted Array**
    - **Leetcode 81 – Search in Rotated Sorted Array II**
    - **Leetcode 153 – Find Minimum in Rotated Sorted Array**
1. [[Search in rotated sorted array]]
2. [[Search in rotated sorted array ii]]
3. [[Find Minimum in Rotated Sorted Array]]

---

## **4️⃣ Binary Search on Answer (Optimization Problems)**

- **Problem Type:** Find the **minimum/maximum feasible value** in a given range.
- **Key Idea:** Instead of searching for an index, **search for a numerical answer**.
- **Examples:**
    - **Leetcode 410 – Split Array Largest Sum** (Minimize the maximum sum among `k` subarrays)
    - **Leetcode 1011 – Capacity to Ship Packages Within D Days**
    - **Leetcode 875 – Koko Eating Bananas** (Find the minimum eating speed)
1. [[Binary search on answer pattern]]
2. [[Koko eating bananas]]
3. [[Capacity to ship packages in D days]]
4. [[Aggresive cows]]
5. [[Magnetic force between balls]]

---

## **5️⃣ Binary Search on Real Numbers (Floating Point Binary Search)**

- **Problem Type:** Find an approximate answer to a **floating-point problem**.
- **Key Idea:** Use binary search with precision (`1e-6`).
- **Examples:**
    - **Square Root Approximation**
    - **Leetcode 69 – Sqrt(x)** (Find integer square root)
    - **Leetcode 373 – Kth Smallest Distance Pair** (Binary search over real number distances)

1. [[Sqrt(X)]]

---

## **6️⃣ Search in 2D Space (Matrix Binary Search)**

- **Problem Type:** Binary search in a **sorted matrix**.
- **Key Idea:** Treat a **2D matrix as a sorted 1D array**.
- **Examples:**
    - **Leetcode 74 – Search a 2D Matrix**
    - **Leetcode 240 – Search a 2D Matrix II** (Row-wise & column-wise sorted)

1. [[Search in a 2D matrix]]
2. [[Search in a 2D matrix ii]]

---

## **7️⃣ Finding Peak Elements / Bitonic Search**

- **Problem Type:** Find the **peak** or **maximum element** in a special array.
- **Key Idea:** Use binary search to move towards the peak.
- **Examples:**
    - **Leetcode 162 – Find Peak Element** (Find a local maximum)
    - **Leetcode 852 – Peak Index in a Mountain Array** (Bitonic Array Search)

1. [[Find peak element]]
2. [[Peak index in mountain array]]

---

## **8️⃣ Kth Smallest/Largest Using Binary Search**

- **Problem Type:** Find the `k`th smallest or largest element efficiently.
- **Key Idea:** Binary search on the **value range** instead of indices.
- **Examples:**
    - **Leetcode 378 – Kth Smallest Element in a Sorted Matrix**
    - **Leetcode 668 – Kth Smallest Number in Multiplication Table**

1. [[Kth smallest in sorted matrix]]
2. [[Kth largest in sorted matrix]]

---

## **9️⃣ Binary Search on Infinite Sorted Arrays**

- **Problem Type:** Search in a **sorted array of unknown size**.
- **Key Idea:** **Exponential expansion** of the search boundary before binary search.
- **Examples:**
    - **Leetcode 702 – Search in a Sorted Infinite Array** (Google Interview Question)

1. [[Binary search in infinite array]]
2. 

---

## **1️⃣1️⃣ Painter’s Partition Problem**

- **Problem Type:** Distribute `n` jobs among `k` workers to minimize the **maximum workload**.
- **Key Idea:** Binary search on the **maximum work** assigned to any worker.
- **Examples:**
    - **Leetcode 410 – Split Array Largest Sum**
    - **Painter’s Partition (Popular in CP)**

---

## **1️⃣2️⃣ Hardest Binary Search Problems (Advanced)**

- **Leetcode 4 – Median of Two Sorted Arrays** (Binary search on two arrays)
- **Leetcode 786 – K-th Smallest Prime Fraction**
- **Leetcode 719 – Find K-th Smallest Pair Distance**
- **Leetcode 222 – Count Complete Tree Nodes (Binary Search on Trees)**

---

## **Final Summary: Binary Search Patterns**

|**Pattern**|**Example Problem**|**Key Idea**|
|---|---|---|
|**Exact Match Search**|**Leetcode 704 – Binary Search**|Standard search in sorted array|
|**First/Last Occurrence**|**Leetcode 34 – First and Last Position**|Lower and upper bound|
|**Rotated Sorted Array**|**Leetcode 33 – Search in Rotated Sorted Array**|Identify pivot|
|**Binary Search on Answer**|**Leetcode 875 – Koko Eating Bananas**|Optimize a function|
|**Floating Point Search**|**Leetcode 69 – Sqrt(x)**|Approximate search|
|**2D Matrix Search**|**Leetcode 74 – Search a 2D Matrix**|Treat as a sorted 1D array|
|**Peak Finding**|**Leetcode 162 – Find Peak Element**|Move towards the peak|
|**Kth Smallest/Largest**|**Leetcode 378 – Kth Smallest in Matrix**|Binary search on value range|
|**Infinite Array Search**|**Leetcode 702 – Search in Infinite Array**|Exponential expansion|
|**Aggressive Cows**|**Leetcode 1552 – Magnetic Force Between Balls**|Maximize minimum distance|
|**Painter’s Partition**|**Leetcode 410 – Split Array Largest Sum**|Distribute workload efficiently|

---