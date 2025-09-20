### **Quick Revision Notes: Maximum (or Minimum) Sum of a Subarray of Size K**

#### **1. Problem Statement**

- Given an array `arr[]` of size `n` and an integer `k`, find the **maximum (or minimum) sum** of any contiguous subarray of size `k`.

---

#### **2. Brute Force Approach - O(n2)O(n^2)**

- **Iterate through all subarrays of size `k`** and compute their sum.
- **Time Complexity:** O(n2)O(n^2) (nested loop).

**Code:**

```java
public static int maxSumBruteForce(int[] arr, int k) {
    int maxSum = Integer.MIN_VALUE;
    for (int i = 0; i <= arr.length - k; i++) {
        int sum = 0;
        for (int j = i; j < i + k; j++) {
            sum += arr[j];
        }
        maxSum = Math.max(maxSum, sum);
    }
    return maxSum;
}
```

---

#### **3. Optimized Approach - Sliding Window - O(n)

- **Use a running sum (window sum)**: Compute the sum of the first `k` elements.
- **Slide the window** by adding the next element and removing the first element of the previous window.
- **Time Complexity:** O(n)O(n) (single pass).

**Code:**

```java
public static int maxSumSlidingWindow(int[] arr, int k) {
    int maxSum = 0, windowSum = 0;

    // Compute the sum of the first K elements
    for (int i = 0; i < k; i++) {
        windowSum += arr[i];
    }
    
    maxSum = windowSum;

    // Slide the window across the array
    for (int i = k; i < arr.length; i++) {
        windowSum += arr[i] - arr[i - k];  // Add new element, remove old element
        maxSum = Math.max(maxSum, windowSum);
    }

    return maxSum;
}
```

---

#### **4. For Minimum Sum Variation**

- **Same sliding window approach**, just track `minSum` instead of `maxSum`.

**Code:**

```java
public static int minSumSlidingWindow(int[] arr, int k) {
    int minSum = 0, windowSum = 0;

    for (int i = 0; i < k; i++) {
        windowSum += arr[i];
    }

    minSum = windowSum;

    for (int i = k; i < arr.length; i++) {
        windowSum += arr[i] - arr[i - k];
        minSum = Math.min(minSum, windowSum);
    }

    return minSum;
}
```

---

#### **5. Key Takeaways**

✅ **Brute Force:** Try all subarrays → O(n2)O(n^2)  
✅ **Sliding Window:** Maintain a running sum and slide the window → O(n)O(n)  
✅ **Works for both Maximum & Minimum Sum by tracking `maxSum` or `minSum`.**

Let me know if you need further clarifications!