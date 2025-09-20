## **Next Greater Element II – Leetcode 503**

### **Problem Statement**

You are given a **circular** array **nums** (meaning after the last element, it wraps around to the first).  
Find the **next greater element** for each element in **nums**.

- The **next greater element** of an element **x** is the first greater number to its **right**.
    
- If no greater number exists, return `-1`.
    

---

### **Example 1**

```text
Input: nums = [1, 2, 1]  
Output: [2, -1, 2]  
Explanation:
- 1 → First greater is 2 → `2`
- 2 → No greater element → `-1`
- 1 (circular) → First greater is 2 → `2`
```

### **Example 2**

```text
Input: nums = [5, 4, 3, 2, 1]  
Output: [-1, -1, -1, -1, -1]  
Explanation: No greater elements exist.
```

---

## **Approach: Using a Monotonic Stack**

### **Key Idea**

Since the array is **circular**, an element at the **beginning** might have its next greater element **later in the array**.  
To handle this efficiently, we **simulate looping twice** over the array.

### **Steps**

1. **Use a decreasing monotonic stack**:
    
    - The **stack stores indexes** of elements (not values).
        
    - As we traverse **nums**, we check the stack.
        
    - If the **current number is greater** than the top of the stack, we **resolve** previous elements by storing their next greater elements.
        
    - Push the **current index** into the stack.
        
2. **Simulate circular behavior**:
    
    - Instead of looping twice, we **simulate** it by iterating **twice the length** of nums (`2n`).
        
    - We use `i % n` to access elements cyclically.
        

---

## **Code (Optimized O(n) Solution)**

```java
import java.util.Arrays;
import java.util.Stack;

class Solution {
    public int[] nextGreaterElements(int[] nums) {
        int n = nums.length;
        int[] result = new int[n];
        Arrays.fill(result, -1); // Default all values to -1

        Stack<Integer> stack = new Stack<>();

        // Traverse the array twice to simulate circular behavior
        for (int i = 0; i < 2 * n; i++) {
            while (!stack.isEmpty() && nums[stack.peek()] < nums[i % n]) {
                result[stack.pop()] = nums[i % n]; // Resolve NGE
            }
            if (i < n) stack.push(i); // Push only during first pass
        }

        return result;
    }

    public static void main(String[] args) {
        Solution sol = new Solution();
        int[] nums = {1, 2, 1};
        System.out.println(Arrays.toString(sol.nextGreaterElements(nums))); // Output: [2, -1, 2]
    }
}
```

---

## **Dry Run**

### **Example:** nums = `[1, 2, 1]`

1. **Processing `nums` normally (i = 0 to n-1)**
    
    ```
    Stack: [0] (1 pushed)
    Stack: [1] (1 < 2 → resolve: result[0] = 2)
    Stack: [1,2] (2 pushed)
    ```
    
2. **Processing circular part (i = n to 2n-1)**
    
    ```
    i = 2 → 1 (no stack updates)
    i = 3 → 2 (stack updated, but no new resolutions)
    i = 4 → 1 (stack empty, nothing happens)
    ```
    

🔹 **Final Result:** `[2, -1, 2]`

---

## **Complexity Analysis**

|Operation|Time Complexity|Explanation|
|---|---|---|
|**Processing nums**|**O(n)**|Each element is pushed/popped at most once|
|**Overall Complexity**|**O(n)**|Traversing twice doesn't change O(n)|

---

## **Comparison of Approaches**

|Approach|Time Complexity|Space Complexity|Best Use Case|
|---|---|---|---|
|**Brute Force**|**O(n²)**|**O(1)**|Small inputs|
|**Monotonic Stack**|**O(n)**|**O(n)**|Large inputs, circular behavior|

---

## **Similar Problems**

- **Next Greater Element I** – Leetcode 496
    
- **Next Smaller Element**
    
- **Stock Span Problem**
    
- **Daily Temperatures** – Leetcode 739
    

---

## **Final Takeaways**

- **Stack stores indices** to efficiently track previous elements.
    
- **Looping twice simulates circular behavior** without extra space.
    
- **O(n) solution is optimal** for large inputs.
    

Let me know if you want more examples or dry runs! 🚀