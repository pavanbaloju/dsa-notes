### **Count Distinct Elements in Every Window of Size K – Revision Notes**

#### **1. Problem Statement**

Given an array `arr[]` of size `n` and an integer `k`, find the **count of distinct elements in every contiguous subarray (window) of size `k`**.

---

### **2. Naive Approach – Brute Force (O(n*k))**

- Iterate through each subarray of size `k`.
- Use a **set** to store distinct elements and count them.
- **Time Complexity:** **O(n*k)** (since checking uniqueness in each window takes O(k)).

#### **Brute Force Code:**

```java
public static void countDistinctBruteForce(int[] arr, int k) {
    for (int i = 0; i <= arr.length - k; i++) {
        Set<Integer> set = new HashSet<>();
        for (int j = i; j < i + k; j++) {
            set.add(arr[j]); // Store unique elements
        }
        System.out.print(set.size() + " ");
    }
}
```

✅ **Works, but inefficient for large inputs (`n ≤ 10⁶`).**

---

### **3. Optimized Approach – Sliding Window + HashMap (O(n))**

#### **Key Idea:**

- Use a **HashMap** to keep track of **frequencies of elements** in the current window.
- **Sliding Window Mechanism:**
    1. **Expand** the window by adding `arr[right]` to the frequency map.
    2. **Remove** the leftmost element (`arr[left]`) from the map when moving forward.
    3. The **size of the map gives the distinct count** at each step.
- **Time Complexity:** **O(n)** (each element is processed only twice).

#### **Optimized Code:**

```java
import java.util.*;

public class CountDistinctElements {
    public static void countDistinctOptimized(int[] arr, int k) {
        Map<Integer, Integer> freqMap = new HashMap<>();
        int distinctCount = 0;

        // Build the first window
        for (int i = 0; i < k; i++) {
            freqMap.put(arr[i], freqMap.getOrDefault(arr[i], 0) + 1);
        }
        System.out.print(freqMap.size() + " ");

        // Process remaining windows
        for (int i = k; i < arr.length; i++) {
            // Remove the leftmost element from the previous window
            int left = arr[i - k];
            if (freqMap.get(left) == 1) {
                freqMap.remove(left);
            } else {
                freqMap.put(left, freqMap.get(left) - 1);
            }

            // Add the new rightmost element
            int right = arr[i];
            freqMap.put(right, freqMap.getOrDefault(right, 0) + 1);

            // Print distinct count for the current window
            System.out.print(freqMap.size() + " ");
        }
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 1, 3, 4, 2, 3};
        int k = 4;
        countDistinctOptimized(arr, k);
        // Output: 3 4 4 3
    }
}
```

---

### **4. Example Walkthrough**

#### **Input:**

```plaintext
arr = [1, 2, 1, 3, 4, 2, 3]
k = 4
```

#### **Window Processing Steps**

|Window|Distinct Elements|Output|
|---|---|---|
|`[1,2,1,3]`|`{1,2,3}`|3|
|`[2,1,3,4]`|`{1,2,3,4}`|4|
|`[1,3,4,2]`|`{1,2,3,4}`|4|
|`[3,4,2,3]`|`{2,3,4}`|3|

✅ **Final Output:** `3 4 4 3`

---

### **5. Time Complexity Analysis**

|**Operation**|**Time Complexity**|
|---|---|
|**Initialize first window** (`O(k)`)|**O(k)**|
|**Sliding window updates (`O(1)` per element)**|**O(n - k)**|
|**Total Complexity**|**O(n)**|

---

### **6. Key Takeaways**

✅ **Brute force takes O(n*k), while sliding window + hashmap reduces it to O(n).**  
✅ **HashMap efficiently tracks element frequencies in the current window.**  
✅ **Each element is processed twice (added and removed), leading to O(n) complexity.**  
✅ **Works efficiently even for large inputs (`n ≤ 10⁶`).**

Would you like any variations of this problem? Let me know!