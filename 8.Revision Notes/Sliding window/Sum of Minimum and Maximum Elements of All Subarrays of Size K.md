### **Sum of Minimum and Maximum Elements of All Subarrays of Size K**

#### **1. Problem Statement**

Given an array `arr[]` of size `n` and an integer `k`, find the sum of the **minimum and maximum** elements for all contiguous subarrays of size `k`.

---

#### **2. Brute Force Approach - O(n2)O(n^2)**

- **Iterate through all subarrays of size `k`** and find their minimum and maximum values separately.
- **Time Complexity:** O(n2)O(n^2) (nested loop).

**Code:**

```java
public static int sumOfMinMaxBruteForce(int[] arr, int k) {
    int sum = 0;

    for (int i = 0; i <= arr.length - k; i++) {
        int minVal = Integer.MAX_VALUE, maxVal = Integer.MIN_VALUE;

        for (int j = i; j < i + k; j++) {
            minVal = Math.min(minVal, arr[j]);
            maxVal = Math.max(maxVal, arr[j]);
        }

        sum += (minVal + maxVal);
    }

    return sum;
}
```

---

#### **3. Optimized Approach - Sliding Window + Deque - O(n)O(n)**

- Use **two deques** to efficiently find the **minimum and maximum** in each window:
    - **MinDeque** (stores indices of elements in increasing order, front gives the minimum).
    - **MaxDeque** (stores indices of elements in decreasing order, front gives the maximum).
- Remove elements from deques that are out of the current window.
- **Time Complexity:** O(n)O(n) (each element enters and exits the deque once).

---

#### **4. Optimized Code - Sliding Window + Deque**

```java
import java.util.*;

public static int sumOfMinMaxSlidingWindow(int[] arr, int k) {
    Deque<Integer> minDeque = new ArrayDeque<>();
    Deque<Integer> maxDeque = new ArrayDeque<>();
    int sum = 0;

    for (int i = 0; i < arr.length; i++) {
        // Remove elements out of the current window
        while (!minDeque.isEmpty() && minDeque.peekFirst() < i - k + 1) {
            minDeque.pollFirst();
        }
        while (!maxDeque.isEmpty() && maxDeque.peekFirst() < i - k + 1) {
            maxDeque.pollFirst();
        }

        // Maintain increasing order in minDeque
        while (!minDeque.isEmpty() && arr[minDeque.peekLast()] >= arr[i]) {
            minDeque.pollLast();
        }
        minDeque.offerLast(i);

        // Maintain decreasing order in maxDeque
        while (!maxDeque.isEmpty() && arr[maxDeque.peekLast()] <= arr[i]) {
            maxDeque.pollLast();
        }
        maxDeque.offerLast(i);

        // Process window when size is K
        if (i >= k - 1) {
            sum += arr[minDeque.peekFirst()] + arr[maxDeque.peekFirst()];
        }
    }

    return sum;
}
```

---

### **5. Key Takeaways**

✅ **Brute Force:** Find min/max for each subarray → O(n2)O(n^2)  
✅ **Optimized Approach:** Use **deques** to maintain min/max → O(n)O(n)  
✅ **Deque Approach Works Best**: Efficiently tracks min/max values for each window.

This method is optimal and commonly asked in coding interviews. Let me know if you need further clarifications!