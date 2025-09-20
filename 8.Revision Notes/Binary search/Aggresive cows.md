# **🐄 Aggressive Cows (SPOJ) – Binary Search on Answer**

## **🔹 Problem Statement**

Given `n` stalls (sorted positions) and `k` cows, place the cows in the stalls such that the **minimum distance** between any two cows is maximized.

### **🔹 Key Idea**

- **We do not search for an index**, but a **numerical answer** (the maximum possible minimum distance).
    
- **Use Binary Search on Answer**:
    
    - **Lower Bound (`low`)** = Minimum possible distance (1 or smallest gap).
        
    - **Upper Bound (`high`)** = Maximum possible distance (`arr[n-1] - arr[0]`).
        

---

## **🔹 Steps to Solve**

### **Step 1️⃣ – Sort the Input**

- Given positions should be sorted for binary search logic to work.
    

### **Step 2️⃣ – Apply Binary Search on Distance**

1. **Search space is distance** between cows, not indices.
    
2. Use **binary search on distance** `[low, high]`, where:
    
    - `low = 1` (smallest possible distance)
        
    - `high = max possible distance = arr[n-1] - arr[0]`
        
3. **Check feasibility** of placing `k` cows with `mid` distance:
    
    - Try placing cows greedily, ensuring each is at least `mid` apart.
        
    - If placement is possible, increase distance (`low = mid + 1`).
        
    - Else, decrease (`high = mid - 1`).
        

---

## **🔹 Java Code Implementation**

```java
import java.util.Arrays;

class AggressiveCows {
    public int maxMinDistance(int[] stalls, int k) {
        Arrays.sort(stalls); // Step 1: Sort the stalls

        int low = 1, high = stalls[stalls.length - 1] - stalls[0];
        int result = 0;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (canPlace(stalls, k, mid)) { // Step 2: Check feasibility
                result = mid;
                low = mid + 1;  // Try a larger minimum distance
            } else {
                high = mid - 1; // Try a smaller minimum distance
            }
        }
        return result;
    }

    // Helper function to check if we can place `k` cows with `minDist`
    private boolean canPlace(int[] stalls, int k, int minDist) {
        int count = 1; // Place first cow
        int lastPlaced = stalls[0];

        for (int i = 1; i < stalls.length; i++) {
            if (stalls[i] - lastPlaced >= minDist) {
                count++;
                lastPlaced = stalls[i]; // Place the next cow

                if (count == k) return true; // Successfully placed all cows
            }
        }
        return false;
    }

    public static void main(String[] args) {
        AggressiveCows sol = new AggressiveCows();
        int[] stalls = {1, 2, 8, 4, 9};
        int k = 3;
        System.out.println(sol.maxMinDistance(stalls, k)); // Output: 3
    }
}
```

---

## **🔹 Why Binary Search?**

- **Finding the optimal distance** between placed cows requires an **ordered search space**.
    
- **Brute force would take O(N²)**, but **Binary Search reduces it to `O(N log M)`**, where `M = max distance`.
    

---

## **🔹 Time Complexity**

1. **Sorting the array:** `O(N log N)`
    
2. **Binary search on answer:** `O(log M)`, where `M = arr[n-1] - arr[0]`
    
3. **Checking feasibility (`canPlace`) for each `mid`:** `O(N)`
    

🔹 **Overall Complexity:** `O(N log N) + O(N log M) ≈ O(N log M)`

---

## **🔹 Variations of This Pattern**

| **Problem Name**                                 | **Concept**                                                    |
| ------------------------------------------------ | -------------------------------------------------------------- |
| **Aggressive Cows** (SPOJ)                       | Place `k` cows in `n` stalls maximizing min distance           |
| **Router Placement**                             | Place `k` WiFi routers in `n` buildings for best coverage      |
| **EKO (SPOJ)**                                   | Find max height `h` to cut trees and collect at least `m` wood |
| **Magnetic Force Between Balls (Leetcode 1552)** | Place `k` balls in `n` positions maximizing min magnetic force |

---

## **🔹 Summary**

- **Use Binary Search on Answer** when searching for **maximum of a minimum value**.
    
- **Check feasibility** using **greedy placement**.
    
- **Optimize distance placement problems efficiently** in `O(N log M)` time.
    

🔹 **🚀 Must-Know Pattern for Interview Binary Search Problems!**