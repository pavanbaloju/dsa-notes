### **Maximum of All Subarrays of Size K – Revision Notes**

#### **1. Problem Statement**

Given an array `arr[]` of size `n` and an integer `k`, find the **maximum element in every contiguous subarray (window) of size `k`**.

---

### **2. Naive Approach – Brute Force (O(n*k))**

- Iterate through **each subarray of size `k`**.
- Find the **maximum element** in each subarray using a nested loop.
- **Time Complexity:** **O(n*k)** (since checking max in each window takes O(k)).

#### **Brute Force Code:**

```java
public static void maxSubarrayBruteForce(int[] arr, int k) {
    for (int i = 0; i <= arr.length - k; i++) {
        int maxVal = Integer.MIN_VALUE;
        for (int j = i; j < i + k; j++) {
            maxVal = Math.max(maxVal, arr[j]);
        }
        System.out.print(maxVal + " ");
    }
}
```

✅ **Works, but inefficient for large `n` (`n ≤ 10⁶`).**

---

### **3. Optimized Approach – Sliding Window + Monotonic Deque (O(n))**

#### **Key Idea:**

- Use a **deque (double-ended queue) to store indices** of useful elements.
- **Maintain a decreasing order** in the deque:
    1. **Remove out-of-window elements** from the front.
    2. **Remove smaller elements from the back** (they are useless).
    3. The **front of the deque always contains the max element** for the window.
- **Time Complexity:** **O(n)** (each element is processed at most twice).

---

### **4. Optimized Code:**

```java
import java.util.*;

public class MaxSubarraySizeK {
    public static void maxSlidingWindow(int[] arr, int k) {
        Deque<Integer> deque = new ArrayDeque<>();
        int n = arr.length;

        for (int i = 0; i < n; i++) {
            // Remove elements out of this window
            while (!deque.isEmpty() && deque.peekFirst() < i - k + 1) {
                deque.pollFirst();
            }

            // Remove smaller elements from back (they won’t be needed)
            while (!deque.isEmpty() && arr[deque.peekLast()] <= arr[i]) {
                deque.pollLast();
            }

            // Add current element at the back
            deque.offerLast(i);

            // Start printing results after the first k elements
            if (i >= k - 1) {
                System.out.print(arr[deque.peekFirst()] + " ");
            }
        }
    }

    public static void main(String[] args) {
        int[] arr = {1, 3, -1, -3, 5, 3, 6, 7};
        int k = 3;
        maxSlidingWindow(arr, k);
        // Output: 3 3 5 5 6 7
    }
}
```

---

### **5. Example Walkthrough**

#### **Input:**

```plaintext
arr = [1, 3, -1, -3, 5, 3, 6, 7]
k = 3
```

#### **Window Processing Steps**

|Window|Deque (Indexes)|Max Element|
|---|---|---|
|`[1, 3, -1]`|`[1]` (holds `3`)|`3`|
|`[3, -1, -3]`|`[1, 2]` (holds `3, -1`)|`3`|
|`[-1, -3, 5]`|`[4]` (holds `5`)|`5`|
|`[-3, 5, 3]`|`[4, 5]` (holds `5, 3`)|`5`|
|`[5, 3, 6]`|`[6]` (holds `6`)|`6`|
|`[3, 6, 7]`|`[7]` (holds `7`)|`7`|

✅ **Final Output:** `3 3 5 5 6 7`

---

### **6. Time Complexity Analysis**

|**Operation**|**Time Complexity**|
|---|---|
|**Processing first k elements**|**O(k)**|
|**Sliding window updates (`O(1)` per element)**|**O(n - k)**|
|**Total Complexity**|**O(n)**|

---

### **7. Key Takeaways**

✅ **Brute force takes O(n*k), while sliding window + deque reduces it to O(n).**  
✅ **Deque efficiently tracks max values within the window.**  
✅ **Each element is processed at most twice (added & removed), leading to O(n) complexity.**  
✅ **Handles large constraints (`n ≤ 10⁶`) efficiently.**

Would you like any variations of this problem? Let me know!