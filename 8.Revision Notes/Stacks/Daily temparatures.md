## **🔹 Daily Temperatures - Monotonic Stack Approach**

### **📌 Problem Statement**

You are given an array `temperatures[]`, where `temperatures[i]` represents the temperature on the `i-th` day.  
For each day, find **the number of days** you have to wait until a **warmer temperature** appears.  
If no future day has a warmer temperature, return **0** for that day.

---

## **🔹 Approach: Using Monotonic Decreasing Stack**

### **📌 Key Observations**

- We need to find **next greater elements** for each temperature.
    
- We use a **monotonic decreasing stack** to efficiently track previous indices where a warmer temperature is yet to be found.
    
- The stack stores **indices** (not values) to track their corresponding temperatures efficiently.
    

---

## **🔹 Algorithm (Step-by-Step)**

1. **Initialize a stack (`stk`)** to store indices.
    
2. **Iterate through each temperature (`i` from `0` to `n-1`)**:
    
    - While the **stack is not empty** and `temperatures[i] > temperatures[stk.peek()]`:
        
        - Pop the **top index (`j`)** from the stack.
            
        - Calculate **the wait time** as `i - j` (difference in indices).
            
        - Store it in `result[j]`.
            
    - Push **current index `i`** onto the stack.
        
3. **Return `result` array** (remaining indices in the stack will stay `0` as they have no warmer day).
    

---

## **🔹 Dry Run**

### **Example Input:**

```java
temperatures = [73, 74, 75, 71, 69, 72, 76, 73]
```

|Step|i|Temp[i]|Stack (stk)|Popped Elements|`result` Update|
|---|---|---|---|---|---|
|1|0|73|`[0]`|-|-|
|2|1|74|`[1]`|`0` (since `74 > 73`)|`result[0] = 1`|
|3|2|75|`[2]`|`1` (since `75 > 74`)|`result[1] = 1`|
|4|3|71|`[2,3]`|-|-|
|5|4|69|`[2,3,4]`|-|-|
|6|5|72|`[2,3,5]`|`4` (since `72 > 69`), `3` (since `72 > 71`)|`result[4] = 1`, `result[3] = 2`|
|7|6|76|`[6]`|`5` (since `76 > 72`), `2` (since `76 > 75`)|`result[5] = 1`, `result[2] = 4`|
|8|7|73|`[6,7]`|-|-|

### **Final `result` Array:**

```
[1, 1, 4, 2, 1, 1, 0, 0]
```

Explanation:

- Day **0 → 1** day later → `74` is warmer.
    
- Day **1 → 1** day later → `75` is warmer.
    
- Day **2 → 4** days later → `76` is warmer.
    
- Day **3 → 2** days later → `72` is warmer.
    
- Day **4 → 1** day later → `72` is warmer.
    
- Day **5 → 1** day later → `76` is warmer.
    
- Day **6 → No** warmer temperature → `0`.
    
- Day **7 → No** warmer temperature → `0`.
    

---

## **🔹 Java Code**

```java
import java.util.*;

class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int n = temperatures.length;
        int[] result = new int[n]; // Initialize with 0
        Deque<Integer> stk = new ArrayDeque<>(); // Stack to store indices

        for (int i = 0; i < n; i++) {
            // Maintain a decreasing order in the stack
            while (!stk.isEmpty() && temperatures[i] > temperatures[stk.peek()]) {
                int index = stk.pop(); // Get previous index
                result[index] = i - index; // Compute the number of days to wait
            }
            stk.push(i); // Push current index
        }

        return result;
    }
}
```

---

## **🔹 Complexity Analysis**

- **Time Complexity:** **O(n)**
    
    - Each element is pushed **once** and popped **once** → **O(n) total**.
        
- **Space Complexity:** **O(n)** (Stack stores indices in the worst case).
    

---

## **🔹 Summary**

|**Concept**|**Explanation**|
|---|---|
|**Stack Type**|**Monotonic Decreasing Stack (stores indices)**|
|**When do we pop?**|If `temperatures[i] > temperatures[stk.peek()]` (i.e., found next warmer day)|
|**What happens after popping?**|Assign `i - index` as wait time|
|**What if no warmer temperature exists?**|Those indices remain `0`|
|**Time Complexity**|**O(n)** (Each element pushed & popped at most once)|
|**Space Complexity**|**O(n)** (Stack stores indices)|

This is the **optimal approach** using **monotonic stacks** for solving **Daily Temperatures** efficiently. 🚀