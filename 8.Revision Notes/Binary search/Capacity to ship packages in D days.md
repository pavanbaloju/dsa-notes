### **🔹 Leetcode 1011 – Capacity to Ship Packages Within D Days (Binary Search on Answer) – Quick Revision Notes**

---

## **🔹 Problem Statement**

You are given `n` packages with weights `[w1, w2, ..., wn]` and `D` days to ship them.  
Each day, you must ship some packages (in order), and your ship has a maximum weight capacity.  
Find the **minimum ship capacity** required to deliver all packages within `D` days.

---

## **🔹 Intuition & Key Observations**

- **Brute Force:** Try all possible ship capacities from `max(weights)` to `sum(weights)`, but this is too slow (`O(N * sum(weights))`).
    
- **Binary Search on Answer:** We are searching for the **minimum feasible ship capacity**, so we apply **binary search on capacity**.
    

---

## **🔹 Steps to Solve Using Binary Search**

### **1️⃣ Define the Search Space**

- **Minimum possible capacity (`low`)** → `max(weights)`, because the ship must at least carry the heaviest package.
    
- **Maximum possible capacity (`high`)** → `sum(weights)`, meaning we ship everything in one day.
    

### **2️⃣ Apply Binary Search on Ship Capacity**

- Compute `mid = (low + high) / 2` as the candidate capacity.
    
- Check if we can ship all packages within `D` days using this capacity (`canShip(weights, D, mid)`).
    

### **3️⃣ Implement Feasibility Function (`canShip(capacity)`)**

- Simulate the number of days needed to ship all packages at speed `mid`.
    
- If total days ≤ `D`, it’s **valid**, so try a **smaller capacity** (`high = mid`).
    
- Otherwise, try a **larger capacity** (`low = mid + 1`).
    

### **4️⃣ The Final Answer**

- When `low == high`, it represents the **minimum valid ship capacity** that ensures delivery in `D` days.
    

---

## **🔹 Binary Search Solution**

```java
import java.util.Arrays;

class Solution {
    public int shipWithinDays(int[] weights, int D) {
        int low = Arrays.stream(weights).max().getAsInt();  // At least max(weights)
        int high = Arrays.stream(weights).sum();  // At most sum(weights)

        while (low < high) {
            int mid = low + (high - low) / 2;
            if (canShip(weights, D, mid)) {
                high = mid;  // Try a smaller capacity
            } else {
                low = mid + 1;  // Increase capacity
            }
        }
        return low;  // Minimum valid capacity
    }

    private boolean canShip(int[] weights, int D, int capacity) {
        int days = 1, currentLoad = 0;
        for (int weight : weights) {
            if (currentLoad + weight > capacity) {
                days++;  // Start a new day
                currentLoad = 0;
            }
            currentLoad += weight;
        }
        return days <= D;
    }
}
```

---

## **🔹 Complexity Analysis**

|Approach|Time Complexity|Space Complexity|
|---|---|---|
|**Brute Force (Linear Search on Capacity)**|`O(N * sum(weights))`|`O(1)`|
|**Binary Search on Answer**|`O(N log(sum(weights)))`|`O(1)`|

- **Binary search on `capacity`** runs in `O(log(sum(weights)))`.
    
- **Checking feasibility (`canShip`)** takes `O(N)`.
    
- Total time complexity → `O(N log(sum(weights)))`, which is much faster than brute force.
    

---

## **🔹 Summary**

|Step|Explanation|
|---|---|
|**1️⃣ Define Search Space**|`low = max(weights)`, `high = sum(weights)`|
|**2️⃣ Binary Search on Capacity**|Compute `mid = (low + high) / 2`|
|**3️⃣ Check Feasibility (`canShip(capacity)`)**|Count the number of days needed|
|**4️⃣ Adjust `low` and `high`**|If `mid` is feasible, try smaller capacity (`high = mid`). Otherwise, increase (`low = mid + 1`).|
|**5️⃣ Return `low`**|The smallest valid capacity|

---

## **🔹 Why This Works?**

- **Binary search works because the function is monotonic** (as `capacity` increases, required days decrease).
    
- We always **try the minimum valid ship capacity** by reducing `high` when a solution is found.
    
- This ensures we efficiently find the **smallest possible capacity** that allows shipping in `D` days. 🚀