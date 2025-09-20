### **Sum of All Subarrays of Size K – Revision Notes**

#### **1. Problem Statement**

Given an array `arr[]` of size `n` and an integer `k`, find the **sum of elements in every contiguous subarray (window) of size `k`**.

---

### **2. Naive Approach – Brute Force (O(n*k))**

- Iterate through **each subarray of size `k`**.
- Compute the sum for each window separately using a nested loop.
- **Time Complexity:** **O(n*k)** (since computing sum for each window takes O(k)).

#### **Brute Force Code:**

```java
public static void sumOfSubarraysBruteForce(int[] arr, int k) {
    for (int i = 0; i <= arr.length - k; i++) {
        int sum = 0;
        for (int j = i; j < i + k; j++) {
            sum += arr[j];
        }
        System.out.print(sum + " ");
    }
}
```

✅ **Works but inefficient for large `n` (`n ≤ 10⁶`).**

---

### **3. Optimized Approach – Sliding Window (O(n))**

#### **Key Idea:**

- Use **sliding window technique** to maintain a running sum.
- **Sliding Window Mechanism:**
    1. Compute **sum of the first window** (first `k` elements).
    2. Slide the window by **adding the next element and removing the first element**.
    3. Print the sum at each step.
- **Time Complexity:** **O(n)** (each element is processed only twice: once added, once removed).

---

### **4. Optimized Code (Sliding Window)**

```java
public class SumOfSubarraysK {
    public static void sumOfSubarrays(int[] arr, int k) {
        int n = arr.length;
        int sum = 0;

        // Compute sum of first k elements
        for (int i = 0; i < k; i++) {
            sum += arr[i];
        }
        System.out.print(sum + " ");

        // Process remaining windows
        for (int i = k; i < n; i++) {
            sum += arr[i] - arr[i - k]; // Add new element, remove old element
            System.out.print(sum + " ");
        }
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5, 6, 7, 8, 9};
        int k = 3;
        sumOfSubarrays(arr, k);
        // Output: 6 9 12 15 18 21 24
    }
}
```

---

### **5. Example Walkthrough**

#### **Input:**

```plaintext
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
k = 3
```

#### **Window Processing Steps**

|Step|Window|Sum Calculation|Output|
|---|---|---|---|
|1|`[1,2,3]`|`1+2+3 = 6`|`6`|
|2|`[2,3,4]`|`6 - 1 + 4 = 9`|`9`|
|3|`[3,4,5]`|`9 - 2 + 5 = 12`|`12`|
|4|`[4,5,6]`|`12 - 3 + 6 = 15`|`15`|
|5|`[5,6,7]`|`15 - 4 + 7 = 18`|`18`|
|6|`[6,7,8]`|`18 - 5 + 8 = 21`|`21`|
|7|`[7,8,9]`|`21 - 6 + 9 = 24`|`24`|

✅ **Final Output:** `6 9 12 15 18 21 24`

---

### **6. Time Complexity Analysis**

|**Operation**|**Time Complexity**|
|---|---|
|**Processing first k elements**|**O(k)**|
|**Sliding window updates (`O(1)` per element)**|**O(n - k)**|
|**Total Complexity**|**O(n)**|

---

### **7. Key Takeaways**

✅ **Brute force takes O(n*k), while sliding window reduces it to O(n).**  
✅ **Maintains a rolling sum, adding and removing elements efficiently.**  
✅ **Each element is processed at most twice (once added, once removed).**  
✅ **Works efficiently even for large constraints (`n ≤ 10⁶`).**

Would you like any variations of this problem? Let me know!