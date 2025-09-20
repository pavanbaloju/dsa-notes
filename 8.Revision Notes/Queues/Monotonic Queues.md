# **Monotonic Queues: In-Depth Explanation**

## **1. Definition**

A **Monotonic Queue** is a specialized **double-ended queue (deque)** that maintains elements in either **increasing** or **decreasing** order. It allows **efficient access** to the **minimum or maximum** element in a sliding window or a continuous range **in O(1)** time, making it a powerful tool for optimization.

### **Types of Monotonic Queues**

1. **Monotonic Increasing Queue** (for finding minimums)
    
    - Maintains elements in **increasing** order (smallest at the front).
    - Before inserting a new element, **remove all larger elements** from the back.
    - The **front of the deque always holds the minimum**.
2. **Monotonic Decreasing Queue** (for finding maximums)
    
    - Maintains elements in **decreasing** order (largest at the front).
    - Before inserting a new element, **remove all smaller elements** from the back.
    - The **front of the deque always holds the maximum**.

---

## **2. How to Build a Monotonic Queue**

We use a **deque (double-ended queue)** to maintain the order efficiently.

### **Building a Monotonic Increasing Queue (Min Queue)**

```java
import java.util.*;

public class MonotonicIncreasingQueue {
    Deque<Integer> deque = new ArrayDeque<>();
    
    // Insert an element while maintaining increasing order
    public void push(int num) {
        while (!deque.isEmpty() && deque.peekLast() > num) {
            deque.pollLast();
        }
        deque.offerLast(num);
    }

    // Get the minimum element in O(1) (it's always at the front)
    public int getMin() {
        return deque.peekFirst();
    }

    // Remove an element (only if it matches the front)
    public void pop(int num) {
        if (!deque.isEmpty() && deque.peekFirst() == num) {
            deque.pollFirst();
        }
    }
}
```

✅ **Front of the deque always holds the minimum element**.

---

### **Building a Monotonic Decreasing Queue (Max Queue)**

```java
import java.util.*;

public class MonotonicDecreasingQueue {
    Deque<Integer> deque = new ArrayDeque<>();
    
    // Insert an element while maintaining decreasing order
    public void push(int num) {
        while (!deque.isEmpty() && deque.peekLast() < num) {
            deque.pollLast();
        }
        deque.offerLast(num);
    }

    // Get the maximum element in O(1)
    public int getMax() {
        return deque.peekFirst();
    }

    // Remove an element (only if it matches the front)
    public void pop(int num) {
        if (!deque.isEmpty() && deque.peekFirst() == num) {
            deque.pollFirst();
        }
    }
}
```

✅ **Front of the deque always holds the maximum element**.

---

## **3. Use Cases of Monotonic Queues**

### **(A) Sliding Window Maximum / Minimum (Most Common Use Case)**

- **Problem:** Find the max (or min) in every window of size `k` in an array.
- **Why Monotonic Queue?** Maintains the order efficiently and ensures `O(n)` complexity.

#### **Sliding Window Maximum using Monotonic Queue (Deque)**

```java
public static int[] maxSlidingWindow(int[] nums, int k) {
    Deque<Integer> deque = new ArrayDeque<>();
    int[] result = new int[nums.length - k + 1];

    for (int i = 0; i < nums.length; i++) {
        // Remove elements that are out of the current window
        while (!deque.isEmpty() && deque.peekFirst() < i - k + 1) {
            deque.pollFirst();
        }

        // Maintain decreasing order: remove smaller elements
        while (!deque.isEmpty() && nums[deque.peekLast()] <= nums[i]) {
            deque.pollLast();
        }

        // Insert current element
        deque.offerLast(i);

        // Store the max value when we have a full window
        if (i >= k - 1) {
            result[i - k + 1] = nums[deque.peekFirst()];
        }
    }

    return result;
}
```

✅ **Time Complexity:** **O(n)** (Each element is added and removed at most once).

---

### **(B) Sum of Minimum & Maximum Elements of All Subarrays of Size K**

- Uses both **monotonic increasing** and **monotonic decreasing queues**.

```java
public static int sumOfMinMax(int[] arr, int k) {
    Deque<Integer> minDeque = new ArrayDeque<>();
    Deque<Integer> maxDeque = new ArrayDeque<>();
    int sum = 0;

    for (int i = 0; i < arr.length; i++) {
        while (!minDeque.isEmpty() && minDeque.peekFirst() < i - k + 1) {
            minDeque.pollFirst();
        }
        while (!maxDeque.isEmpty() && maxDeque.peekFirst() < i - k + 1) {
            maxDeque.pollFirst();
        }

        while (!minDeque.isEmpty() && arr[minDeque.peekLast()] >= arr[i]) {
            minDeque.pollLast();
        }
        minDeque.offerLast(i);

        while (!maxDeque.isEmpty() && arr[maxDeque.peekLast()] <= arr[i]) {
            maxDeque.pollLast();
        }
        maxDeque.offerLast(i);

        if (i >= k - 1) {
            sum += arr[minDeque.peekFirst()] + arr[maxDeque.peekFirst()];
        }
    }

    return sum;
}
```

✅ **Efficient `O(n)` approach for range sum queries**.

---

### **(C) Longest Subarray with Absolute Difference ≤ Limit**

- Uses **both min and max queues** to track the valid range dynamically.

```java
public static int longestSubarray(int[] nums, int limit) {
    Deque<Integer> maxDeque = new ArrayDeque<>();
    Deque<Integer> minDeque = new ArrayDeque<>();
    int left = 0, maxLength = 0;

    for (int right = 0; right < nums.length; right++) {
        while (!maxDeque.isEmpty() && nums[maxDeque.peekLast()] <= nums[right]) {
            maxDeque.pollLast();
        }
        maxDeque.offerLast(right);

        while (!minDeque.isEmpty() && nums[minDeque.peekLast()] >= nums[right]) {
            minDeque.pollLast();
        }
        minDeque.offerLast(right);

        while (nums[maxDeque.peekFirst()] - nums[minDeque.peekFirst()] > limit) {
            left++;
            if (maxDeque.peekFirst() < left) maxDeque.pollFirst();
            if (minDeque.peekFirst() < left) minDeque.pollFirst();
        }

        maxLength = Math.max(maxLength, right - left + 1);
    }

    return maxLength;
}
```

✅ **Efficient `O(n)` approach for range queries with constraints**.

---

## **4. Advantages of Monotonic Queue**

|**Advantage**|**Why?**|
|---|---|
|**O(1) Min/Max Retrieval**|The front of the deque always stores the min/max.|
|**O(n) Complexity**|Each element is added/removed at most once.|
|**Avoids Sorting or Extra Data Structures**|More efficient than heaps or sorting.|
|**Great for Sliding Window Problems**|Optimized for problems with dynamic windows.|

---

## **5. Summary & Takeaways**

✅ **Monotonic Queue maintains elements in increasing or decreasing order** using a **deque**.  
✅ **Used in Sliding Window Max/Min, Range Queries, Longest Subarrays with Constraints.**  
✅ **Efficient O(n) alternative to brute-force O(n²) solutions.**  
✅ **Alternative to segment trees or priority queues for range min/max queries.**

Would you like more practice problems or further clarifications? Let me know!