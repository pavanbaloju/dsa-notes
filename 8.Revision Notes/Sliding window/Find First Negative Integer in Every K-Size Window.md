### **Find First Negative Integer in Every K-Size Window – Revision Notes**

#### **1. Problem Statement**

Given an array `arr[]` of size `n` and an integer `k`, find the **first negative integer** in every contiguous subarray (window) of size `k`.

- If there is no negative integer in a window, return `0` for that window.

---

### **2. Naive Approach – Brute Force (O(n*k))**

- Iterate through all subarrays of size `k`.
- Check for the first negative integer in each window.
- **Time Complexity:** **O(n*k)** (nested loop).

#### **Brute Force Code:**

```java
public static void firstNegativeBruteForce(int[] arr, int k) {
    for (int i = 0; i <= arr.length - k; i++) {
        boolean found = false;
        for (int j = i; j < i + k; j++) {
            if (arr[j] < 0) {
                System.out.print(arr[j] + " ");
                found = true;
                break;
            }
        }
        if (!found) System.out.print("0 ");
    }
}
```

✅ **Works, but inefficient for large `n` (`n ≤ 10⁶`).**

---

### **3. Optimized Approach – Sliding Window + Queue (O(n))**

#### **Key Idea:**

- Use a **queue (Deque) to track negative numbers** in the current window.
- **Sliding Window Mechanism:**
    1. Add **indices of negative numbers** in the window into the queue.
    2. If the front of the queue **is out of the window**, remove it.
    3. The **front of the queue gives the first negative integer** for the current window.
    4. If no negative number exists in the window, print `0`.
- **Time Complexity:** **O(n)** (each element is processed at most twice).

---

### **4. Optimized Code:**

```java
import java.util.*;

public class FirstNegativeInWindow {
    public static void firstNegativeOptimized(int[] arr, int k) {
        Deque<Integer> deque = new ArrayDeque<>();
        int n = arr.length;

        // Process first k elements
        for (int i = 0; i < k; i++) {
            if (arr[i] < 0) deque.offerLast(i);
        }

        // Process remaining elements
        for (int i = k; i < n; i++) {
            // Print first negative element in the current window
            System.out.print(deque.isEmpty() ? "0 " : arr[deque.peekFirst()] + " ");

            // Remove elements that are out of the window
            if (!deque.isEmpty() && deque.peekFirst() < i - k + 1) {
                deque.pollFirst();
            }

            // Add current element if it's negative
            if (arr[i] < 0) {
                deque.offerLast(i);
            }
        }

        // Print last window result
        System.out.print(deque.isEmpty() ? "0 " : arr[deque.peekFirst()] + " ");
    }

    public static void main(String[] args) {
        int[] arr = {12, -1, -7, 8, -15, 30, 16, 28};
        int k = 3;
        firstNegativeOptimized(arr, k);
        // Output: -1 -1 -7 -15 -15 0
    }
}
```

---

### **5. Example Walkthrough**

#### **Input:**

```plaintext
arr = [12, -1, -7, 8, -15, 30, 16, 28]
k = 3
```

#### **Window Processing Steps**

|Window|Queue (`deque`)|First Negative|
|---|---|---|
|`[12, -1, -7]`|`[-1, -7]`|`-1`|
|`[-1, -7, 8]`|`[-1, -7]`|`-1`|
|`[-7, 8, -15]`|`[-7, -15]`|`-7`|
|`[8, -15, 30]`|`[-15]`|`-15`|
|`[-15, 30, 16]`|`[-15]`|`-15`|
|`[30, 16, 28]`|`[]` (no negatives)|`0`|

✅ **Final Output:** `-1 -1 -7 -15 -15 0`

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
✅ **Deque efficiently tracks negative numbers within the window.**  
✅ **Each element is processed at most twice (added & removed), leading to O(n) complexity.**  
✅ **Handles large constraints (`n ≤ 10⁶`) efficiently.**

Would you like any variations of this problem? Let me know!