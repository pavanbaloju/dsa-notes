### **Leetcode 209: Minimum Size Subarray Sum – Revision Notes**

---

## **1. Problem Statement**

Given an array `arr[]` of size `n` and an integer `target`, find the **minimum length** of a contiguous subarray whose sum is **greater than or equal to `target`**.

- If no such subarray exists, return `0`.

---

## **2. Naive Approach – Brute Force (O(n²))**

- Iterate through **all possible subarrays**.
- Check if the sum of each subarray is **≥ target**.
- Keep track of the **smallest valid subarray length**.
- **Time Complexity:** **O(n²)** (inefficient for large inputs).

#### **Brute Force Code:**

```java
public static int minSubArrayLenBruteForce(int target, int[] arr) {
    int minLength = Integer.MAX_VALUE;

    for (int i = 0; i < arr.length; i++) {
        int sum = 0;
        for (int j = i; j < arr.length; j++) {
            sum += arr[j];
            if (sum >= target) {
                minLength = Math.min(minLength, j - i + 1);
                break;  // No need to check further as subarray only grows
            }
        }
    }

    return (minLength == Integer.MAX_VALUE) ? 0 : minLength;
}
```

✅ **Works for small `n`, but too slow for large `n` (`n ≤ 10⁵`).**

---

## **3. Optimized Approach – Sliding Window (O(n))**

### **Key Idea:**

- **Expand (`end++`)** the window until the sum **≥ target**.
- Once valid, **shrink (`start++`)** to find the **minimum window** that still satisfies the condition.
- **Update `minLength`** whenever a valid subarray is found.
- **Time Complexity:** **O(n)** (each element processed at most twice).

---

### **4. Optimized Code (Sliding Window)**

```java
public class MinSizeSubarraySum {
    public static int minSubArrayLen(int target, int[] arr) {
        int start = 0, sum = 0, minLength = Integer.MAX_VALUE;

        for (int end = 0; end < arr.length; end++) {
            sum += arr[end];

            // Try to shrink the window while sum ≥ target
            while (sum >= target) {
                minLength = Math.min(minLength, end - start + 1);
                sum -= arr[start];
                start++;
            }
        }

        return (minLength == Integer.MAX_VALUE) ? 0 : minLength;
    }

    public static void main(String[] args) {
        int[] arr = {2, 3, 1, 2, 4, 3};
        int target = 7;
        System.out.println("Minimum subarray length: " + minSubArrayLen(target, arr));
        // Output: 2 (subarray: [4,3])
    }
}
```

---

### **5. Example Walkthrough**

#### **Input:**

```plaintext
arr = [2, 3, 1, 2, 4, 3], target = 7
```

#### **Window Processing Steps**

|Step|`end`|`start`|Current Window|Sum|Min Length|
|---|---|---|---|---|---|
|1|`0`|`0`|`[2]`|`2`|-|
|2|`1`|`0`|`[2,3]`|`5`|-|
|3|`2`|`0`|`[2,3,1]`|`6`|-|
|4|`3`|`0`|`[2,3,1,2]`|`8` ✅|`4`|
|5|`3`|`1`|`[3,1,2]`|`6`|`4`|
|6|`4`|`1`|`[3,1,2,4]`|`10` ✅|`4`|
|7|`4`|`2`|`[1,2,4]`|`9` ✅|`3`|
|8|`4`|`3`|`[2,4]`|`6`|`3`|
|9|`5`|`3`|`[2,4,3]`|`9` ✅|`3`|
|10|`5`|`4`|`[4,3]`|`7` ✅|`2`|

✅ **Final Output:** `2` (Subarray: `[4,3]`)

---

### **6. Time Complexity Analysis**

|**Operation**|**Time Complexity**|
|---|---|
|**Processing each character once**|**O(n)**|
|**Updating Window**|**O(1) per update**|
|**Total Complexity**|**O(n)**|

---

### **7. Alternative Approach – Binary Search (O(n log n))**

- **Convert the problem into a Prefix Sum + Binary Search**.
- **Precompute prefix sums**, then use **binary search** to find the minimum subarray.
- **Time Complexity:** **O(n log n)** (better for very large `n`).

#### **Binary Search Code:**

```java
import java.util.*;

public class MinSizeSubarraySumBinarySearch {
    public static int minSubArrayLen(int target, int[] arr) {
        int n = arr.length;
        int[] prefixSum = new int[n + 1];

        for (int i = 1; i <= n; i++) {
            prefixSum[i] = prefixSum[i - 1] + arr[i - 1];
        }

        int minLength = Integer.MAX_VALUE;
        for (int i = 0; i < n; i++) {
            int requiredSum = target + prefixSum[i];
            int bound = Arrays.binarySearch(prefixSum, requiredSum);
            if (bound < 0) bound = -bound - 1;
            if (bound <= n) {
                minLength = Math.min(minLength, bound - i);
            }
        }

        return (minLength == Integer.MAX_VALUE) ? 0 : minLength;
    }
}
```

✅ **Useful when `n` is extremely large (`n ≈ 10⁶`) and binary search optimizations are required.**

---

### **8. Summary of Approaches**

|**Approach**|**Time Complexity**|**Space Complexity**|**When to Use?**|
|---|---|---|---|
|**Brute Force (Nested Loops)**|**O(n²)**|**O(1)**|Small constraints (`n ≤ 10³`)|
|**Sliding Window (Optimal)**|**O(n)**|**O(1)**|Best for `n ≤ 10⁵`, efficient|
|**Binary Search + Prefix Sum**|**O(n log n)**|**O(n)**|Best for extremely large `n` (`n ≤ 10⁶`)|

---

### **9. Key Takeaways**

✅ **Sliding Window reduces O(n²) brute force to O(n).**  
✅ **Binary Search alternative is useful when `n` is very large.**  
✅ **Each element is processed at most twice in the sliding window approach.**  
✅ **Handles large constraints (`n ≤ 10⁵`) efficiently.**

Would you like a detailed breakdown of the **binary search approach** or another variation of this problem? 🚀