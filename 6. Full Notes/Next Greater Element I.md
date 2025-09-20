## **Next Greater Element I – Leetcode 496**

### **Problem Statement**

You are given two arrays **nums1** and **nums2** where **nums1** is a subset of **nums2**. Find the **next greater element** for each element in **nums1** using **nums2**.

- The **next greater element** of an element **x** in **nums2** is the first greater number to its right.
    
- If no such number exists, return `-1`.
    

🔹 **Example 1**

```text
Input: nums1 = [4,1,2], nums2 = [1,3,4,2]  
Output: [-1, 3, -1]  
Explanation:  
- 4 → No greater element on right → `-1`  
- 1 → First greater is 3 → `3`  
- 2 → No greater element on right → `-1`
```

🔹 **Example 2**

```text
Input: nums1 = [2,4], nums2 = [1,2,3,4]  
Output: [3, -1]  
Explanation:  
- 2 → First greater is 3 → `3`  
- 4 → No greater element → `-1`
```

---

## **Approach 1️⃣: Brute Force (O(n²))**

### **Explanation**

- For each element in **nums1**, find its index in **nums2**.
    
- Start searching to the **right** for the next greater element.
    
- If found, store it; otherwise, store `-1`.
    

### **Code**

```java
import java.util.Arrays;

class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        int[] result = new int[nums1.length];

        for (int i = 0; i < nums1.length; i++) {
            int num = nums1[i];
            int idx = -1;

            // Find index of nums1[i] in nums2
            for (int j = 0; j < nums2.length; j++) {
                if (nums2[j] == num) {
                    idx = j;
                    break;
                }
            }

            // Search for next greater element
            int nge = -1;
            for (int j = idx + 1; j < nums2.length; j++) {
                if (nums2[j] > num) {
                    nge = nums2[j];
                    break;
                }
            }

            result[i] = nge;
        }
        return result;
    }

    public static void main(String[] args) {
        Solution sol = new Solution();
        int[] nums1 = {4,1,2}, nums2 = {1,3,4,2};
        System.out.println(Arrays.toString(sol.nextGreaterElement(nums1, nums2))); // Output: [-1, 3, -1]
    }
}
```

✅ **Simple to understand**  
❌ **O(n²) time complexity** → Slow for large inputs

---

## **Approach 2️⃣: Using a Monotonic Stack (O(n) Time)**

### **Key Idea**

- We use a **decreasing monotonic stack** to process **nums2** efficiently in **O(n)** time.
    
- The stack keeps track of elements **whose next greater element hasn’t been found yet**.
    
- As we traverse **nums2**, whenever we encounter a greater element, we resolve previous elements in the stack.
    

### **Steps**

1. **Process nums2 using a stack**:
    
    - Traverse **nums2** from **left to right**.
        
    - Maintain a **monotonic decreasing stack** (top stores the smallest element).
        
    - When a new element is **greater than the stack’s top**, that means we found a **next greater element** for all elements in the stack.
        
    - Store the mapping `{element → next greater element}` in a **HashMap**.
        
    - Push the new element onto the stack.
        
2. **Look up values for nums1** using the precomputed HashMap.
    

---

### **Code**

```java
import java.util.*;

class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        Map<Integer, Integer> ngeMap = new HashMap<>();
        Stack<Integer> stack = new Stack<>();

        // Process nums2 to find NGE using stack
        for (int num : nums2) {
            while (!stack.isEmpty() && stack.peek() < num) {
                ngeMap.put(stack.pop(), num);
            }
            stack.push(num);
        }

        // Fill result for nums1 using precomputed values
        int[] result = new int[nums1.length];
        for (int i = 0; i < nums1.length; i++) {
            result[i] = ngeMap.getOrDefault(nums1[i], -1);
        }

        return result;
    }

    public static void main(String[] args) {
        Solution sol = new Solution();
        int[] nums1 = {4,1,2}, nums2 = {1,3,4,2};
        System.out.println(Arrays.toString(sol.nextGreaterElement(nums1, nums2))); // Output: [-1, 3, -1]
    }
}
```

---

## **Dry Run**

### **Example:** nums1 = `[4,1,2]`, nums2 = `[1,3,4,2]`

1. **Process nums2 using Stack**
    
    ```
    Stack: [1]         (1 pushed)
    Stack: [3]         (1 < 3 → store {1 → 3}, pop 1)
    Stack: [3,4]       (3 < 4 → store {3 → 4}, pop 3)
    Stack: [4,2]       (4 > 2 → push 2)
    ```
    
    **HashMap:** `{1 → 3, 3 → 4}`
    
2. **Retrieve for nums1**
    
    ```
    nums1 = [4,1,2] → [-1, 3, -1]
    ```
    

---

## **Complexity Analysis**

|Operation|Time Complexity|Explanation|
|---|---|---|
|**Processing nums2**|**O(n)**|Each element is pushed/popped at most once|
|**Building result for nums1**|**O(n)**|HashMap lookups are O(1)|
|**Overall Complexity**|**O(n)**|Faster than brute force|

---

## **Comparison of Approaches**

|Approach|Time Complexity|Space Complexity|Best Use Case|
|---|---|---|---|
|**Brute Force**|**O(n²)**|**O(1)**|Small inputs|
|**Monotonic Stack**|**O(n)**|**O(n)** (for HashMap & Stack)|Large inputs|

---

## **Similar Problems**

- **Next Greater Element II (Circular Array)** – Leetcode 503
    
- **Next Smaller Element**
    
- **Daily Temperatures** – Leetcode 739
    
- **Stock Span Problem**
    

---

## **Final Takeaway**

- If asked for **Next Greater Element**, **Monotonic Stack** is often the best approach.
    
- **Brute Force is simple but slow** – use **Stack + HashMap** for an **optimal O(n) solution**.
    
- **Dry run with an example** to understand **how the stack evolves**.
    

Let me know if you want a **detailed dry run** for another example! 🚀