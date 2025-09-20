### **Sliding Window Maximum – Revision Notes**

---

## **1. Problem Statement**

Given an array `arr[]` of size `n` and an integer `k`, find the **maximum element in every contiguous subarray (window) of size `k`**.

---

## **2. Naive Approach – Brute Force (O(n*k))**

- Iterate through **each subarray of size `k`**.
- Find the **maximum element** in each subarray using a nested loop.
- **Time Complexity:** **O(n*k)** (inefficient for large inputs).

#### **Brute Force Code:**

```java
public static void maxSlidingWindowBruteForce(int[] arr, int k) {
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

## **3. Optimized Approach – Monotonic Deque (O(n))**

#### **Key Idea:**

- Use a **Deque (double-ended queue) to store indices** of useful elements.
- **Maintain a decreasing order** in the deque:
    1. **Remove out-of-window elements** from the front.
    2. **Remove smaller elements from the back** (they are useless).
    3. The **front of the deque always contains the max element** for the window.
- **Time Complexity:** **O(n)** (each element is processed at most twice).

---

### **4. Optimized Code (Deque)**

```java
import java.util.*;

public class SlidingWindowMaximum {
    public static int[] maxSlidingWindow(int[] arr, int k) {
        Deque<Integer> deque = new ArrayDeque<>();
        int n = arr.length;
        int[] result = new int[n - k + 1];

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

            // Store the result after first k elements
            if (i >= k - 1) {
                result[i - k + 1] = arr[deque.peekFirst()];
            }
        }

        return result;
    }

    public static void main(String[] args) {
        int[] arr = {1, 3, -1, -3, 5, 3, 6, 7};
        int k = 3;
        System.out.println(Arrays.toString(maxSlidingWindow(arr, k)));
        // Output: [3, 3, 5, 5, 6, 7]
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

✅ **Final Output:** `[3, 3, 5, 5, 6, 7]`

---

### **6. Time Complexity Analysis**

|**Operation**|**Time Complexity**|
|---|---|
|**Processing first k elements**|**O(k)**|
|**Sliding window updates (`O(1)` per element)**|**O(n - k)**|
|**Total Complexity**|**O(n)**|

---

### **7. Alternative Approach – Max Heap (O(n log k))**

- Use a **Max Heap (PriorityQueue)** to track the max element in the window.
- **Pop elements out of the window** when they exceed the left boundary.
- **Time Complexity:** **O(n log k)** (due to heap insertions/removals).

#### **Heap-Based Code:**

```java
import java.util.*;

public class SlidingWindowMaxHeap {
    public static int[] maxSlidingWindow(int[] arr, int k) {
        PriorityQueue<int[]> maxHeap = new PriorityQueue<>((a, b) -> b[0] - a[0]);
        int n = arr.length;
        int[] result = new int[n - k + 1];

        for (int i = 0; i < n; i++) {
            maxHeap.offer(new int[]{arr[i], i});

            if (i >= k - 1) {
                // Remove out-of-window elements
                while (maxHeap.peek()[1] < i - k + 1) {
                    maxHeap.poll();
                }
                result[i - k + 1] = maxHeap.peek()[0];
            }
        }

        return result;
    }

    public static void main(String[] args) {
        int[] arr = {1, 3, -1, -3, 5, 3, 6, 7};
        int k = 3;
        System.out.println(Arrays.toString(maxSlidingWindow(arr, k)));
        // Output: [3, 3, 5, 5, 6, 7]
    }
}
```

✅ **Works, but heap operations make it slower than Deque approach (`O(n log k)`).**

---

### **8. Summary of Approaches**

|**Approach**|**Time Complexity**|**Space Complexity**|**When to Use?**|
|---|---|---|---|
|**Brute Force (Nested Loops)**|**O(n*k)**|**O(1)**|Small constraints (`n ≤ 10³`)|
|**Deque (Monotonic Queue)**|**O(n)**|**O(k)**|Best for `n ≤ 10⁶`, efficient|
|**Max Heap (Priority Queue)**|**O(n log k)**|**O(k)**|If `k` is very small (`k ≤ 50`)|

---

### **9. Key Takeaways**

✅ **Brute force takes O(n*k), while sliding window (Deque) reduces it to O(n).**  
✅ **Deque efficiently tracks max values within the window.**  
✅ **Each element is processed at most twice (added & removed), leading to O(n) complexity.**  
✅ **Heap-based solution is valid but has additional `log k` overhead.**

Would you like any variations of this problem? Let me know! 🚀