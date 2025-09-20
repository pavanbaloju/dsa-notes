### **🔹 Leetcode 875 – Koko Eating Bananas (Binary Search on Answer) – Quick Revision Notes**

#### **🔸 Problem Statement**

Koko loves to eat bananas. There are `n` piles of bananas, where the `i`-th pile has `piles[i]` bananas. Koko has `H` hours to eat all the bananas.  
Each hour, she can eat at most `K` bananas. Find the **minimum eating speed `K`** such that she can finish all bananas in `H` hours.

---

## **🔹 Intuition & Key Observations**

- **Brute Force:** Try all possible speeds from `1` to `max(piles)`, but this is too slow (`O(N * max(piles))`).
    
- **Binary Search on Answer:** We are **searching for the minimum feasible value**, so we apply **binary search on the eating speed `K`**.
    

---

## **🔹 Steps to Solve Using Binary Search**

### **1️⃣ Define the Search Space**

- **Minimum possible speed (`low`)** → `1` (Koko can eat at least 1 banana/hour).
    
- **Maximum possible speed (`high`)** → `max(piles)` (Koko eats the largest pile in 1 hour).
    

### **2️⃣ Apply Binary Search on Eating Speed `K`**

- Compute `mid = (low + high) / 2` as the candidate speed.
    
- Check if she can finish within `H` hours using this speed (`canFinish(mid)`).
    

### **3️⃣ Implement Feasibility Function (`canFinish(K)`)**

- Simulate the total hours required if she eats at speed `K`.
    
- If total hours ≤ `H`, it’s **valid**, so try a **smaller speed** (`high = mid`).
    
- Otherwise, try a **higher speed** (`low = mid + 1`).
    

### **4️⃣ The Final Answer**

- When `low == high`, it represents the **minimum valid speed** at which Koko can finish in `H` hours.
    

---

## **🔹 Binary Search Solution**

```java
import java.util.Arrays;

class Solution {
    public int minEatingSpeed(int[] piles, int h) {
        int low = 1, high = Arrays.stream(piles).max().getAsInt();

        while (low < high) {
            int mid = low + (high - low) / 2;
            if (canFinish(piles, h, mid)) {
                high = mid;  // Try a smaller speed
            } else {
                low = mid + 1;  // Increase speed
            }
        }
        return low;  // Minimum valid eating speed
    }

    private boolean canFinish(int[] piles, int h, int speed) {
        int hours = 0;
        for (int pile : piles) {
            hours += Math.ceil((double) pile / speed); // Compute time for each pile
        }
        return hours <= h;
    }
}
```

---

## **🔹 Complexity Analysis**

|Approach|Time Complexity|Space Complexity|
|---|---|---|
|**Brute Force (Linear Search on K)**|`O(N * max(piles))`|`O(1)`|
|**Binary Search on Answer**|`O(N log(max(piles)))`|`O(1)`|

- **Binary search on `K`** runs in `O(log(max(piles)))`.
    
- **Checking feasibility (`canFinish`)** takes `O(N)`.
    
- Total time complexity → `O(N log(max(piles)))`, which is much faster than brute force.
    

---

## **🔹 Summary**

|Step|Explanation|
|---|---|
|**1️⃣ Define Search Space**|`low = 1`, `high = max(piles)`|
|**2️⃣ Binary Search on `K`**|Compute `mid = (low + high) / 2`|
|**3️⃣ Check Feasibility (`canFinish(K)`)**|Compute hours required to finish bananas|
|**4️⃣ Adjust `low` and `high`**|If `mid` is feasible, try smaller speed (`high = mid`). Otherwise, increase (`low = mid + 1`).|
|**5️⃣ Return `low`**|The smallest valid speed `K`|

---

## **🔹 Why This Works?**

- **Binary search works because the function is monotonic** (as `K` increases, total hours decrease).
    
- We always **try the minimum valid `K`** by reducing `high` when a solution is found.
    
- This ensures we efficiently find the **smallest possible speed** that allows Koko to finish on time. 🚀