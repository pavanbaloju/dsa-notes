## **🔹 Finding Square Root Using Binary Search – Revision Notes**

### **🔹 Problem Statement**

Given a number `x`, find its **square root** up to a given precision using **Binary Search**.

---

### **🔹 Key Idea**

Instead of using `Math.sqrt()`, we can use **binary search** to efficiently find `√x`.

1. The function `f(mid) = mid * mid` is **monotonic**, meaning that as `mid` increases, `mid * mid` also increases.
    
2. This allows us to use **binary search** in the range `[0, x]`.
    
3. We repeatedly narrow the search space until we get the answer with the required precision.
    

---

### **🔹 Steps to Solve Using Binary Search**

1️⃣ **Define the search space `[low, high]`**

- If `x < 1`, set `high = 1` (since `√x` will be greater than `x` but less than `1`).
    
- Otherwise, set `low = 0` and `high = x`.
    

2️⃣ **Perform Binary Search**

- Compute `mid = (low + high) / 2`.
    
- If `mid * mid == x`, return `mid`.
    
- If `mid * mid < x`, move `low = mid`.
    
- Else, move `high = mid`.
    

3️⃣ **Stop when `high - low ≤ precision`**

- Precision is usually `1e-6` (`10⁻⁶`) for real numbers.
    

---

### **🔹 Integer Square Root (Perfect Square)**

If we only need the **integer part** of the square root:

- Use `high = mid - 1` and `low = mid + 1` in a standard binary search.
    

```java
class Solution {
    public int integerSqrt(int x) {
        if (x == 0 || x == 1) return x;
        
        int low = 1, high = x, ans = 0;
        
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (mid * mid == x) return mid;
            if (mid * mid < x) {
                ans = mid; // Store potential answer
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        return ans; // Return the floor value of √x
    }

    public static void main(String[] args) {
        Solution sol = new Solution();
        System.out.println(sol.integerSqrt(10)); // Output: 3
    }
}
```

✅ **Time Complexity:** `O(log x)`  
✅ **Space Complexity:** `O(1)`

---

### **🔹 Floating Point Square Root (Up to 6 Decimal Places)**

If we need **precise values** with decimals:

- Use a `double` and continue binary search **until precision is reached**.
    

```java
class Solution {
    public double sqrtBinarySearch(double x) {
        double low = 0, high = x, precision = 1e-6;
        
        while (high - low > precision) {
            double mid = low + (high - low) / 2;
            if (mid * mid < x) {
                low = mid;
            } else {
                high = mid;
            }
        }
        return low; // or return high
    }

    public static void main(String[] args) {
        Solution sol = new Solution();
        System.out.println(sol.sqrtBinarySearch(10)); // Output: ~3.162278
    }
}
```

✅ **Time Complexity:** `O(log(x / precision))`  
✅ **Space Complexity:** `O(1)`

---

### **🔹 Summary**

|**Step**|**Explanation**|
|---|---|
|**1️⃣ Define Search Space**|`[low, high] = [0, x]` (or `[x, 1]` for `x < 1`).|
|**2️⃣ Perform Binary Search**|Compute `mid = (low + high) / 2`.|
|**3️⃣ Check Condition**|If `mid * mid < x`, move `low = mid`, otherwise move `high = mid`.|
|**4️⃣ Stop When `high - low ≤ precision`**|Use `1e-6` for accuracy.|

This approach is **fast, efficient, and widely used** for finding square roots accurately! 🚀