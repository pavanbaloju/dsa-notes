## **Daily Temperatures (LeetCode 739) – Monotonic Stack Approach**

### **Problem Statement**

Given an array `temperatures[]` where `temperatures[i]` represents the **daily temperature**, return an array `answer[]` where `answer[i]` is **the number of days until a warmer temperature appears**. If no future day has a higher temperature, return `0` for that day.

### **Example**

```java
Input: temperatures = [73,74,75,71,69,72,76,73]
Output: [1,1,4,2,1,1,0,0]
```

#### **Explanation**

- For **`73` (day 0)** → Warmer day in **1 day** (`74` on day 1).
    
- For **`74` (day 1)** → Warmer day in **1 day** (`75` on day 2).
    
- For **`75` (day 2)** → Warmer day in **4 days** (`76` on day 6).
    
- For **`71` (day 3)** → Warmer day in **2 days** (`72` on day 5).
    
- For **`69` (day 4)** → Warmer day in **1 day** (`72` on day 5).
    
- For **`72` (day 5)** → Warmer day in **1 day** (`76` on day 6).
    
- For **`76` (day 6)** → No warmer day exists, so `0`.
    
- For **`73` (day 7)** → No warmer day exists, so `0`.
    

---

## **🔹 Approach 1: Brute Force (O(N²))**

### **Steps**

1. For each `i`, scan **forward** to find the first day `j` where `temperature[j] > temperature[i]`.
    
2. Store `j - i` in `answer[i]`.
    
3. If no higher temperature exists, store `0`.
    

**🔻 Code**

```java
public int[] dailyTemperaturesBruteForce(int[] temperatures) {
    int n = temperatures.length;
    int[] answer = new int[n];

    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            if (temperatures[j] > temperatures[i]) {
                answer[i] = j - i;
                break;
            }
        }
    }
    return answer;
}
```

🔴 **Time Complexity:** **O(N²)** (Inefficient for large `N`)

---

## **🔹 Approach 2: Using Monotonic Decreasing Stack (O(N))**

### **Key Observations**

- We process elements **from left to right**.
    
- **Maintain a decreasing stack** of indices (stores temperatures in decreasing order).
    
- If `temperatures[i] > temperatures[stack.peek()]`, we found a **warmer day**:
    
    - Pop from the stack.
        
    - Compute `answer[stack.pop()] = i - stack.pop()`.
        
- Otherwise, push the current index onto the stack.
    

---

### **📌 Optimized Java Code (O(N))**

```java
import java.util.Stack;

public class DailyTemperatures {
    public int[] dailyTemperatures(int[] temperatures) {
        int n = temperatures.length;
        int[] answer = new int[n];
        Stack<Integer> stack = new Stack<>(); // Stores indices

        for (int i = 0; i < n; i++) {
            // Process all previous days with a lower temperature
            while (!stack.isEmpty() && temperatures[i] > temperatures[stack.peek()]) {
                int prevIndex = stack.pop();
                answer[prevIndex] = i - prevIndex; // Days until a warmer temperature
            }
            stack.push(i); // Push current day's index onto stack
        }

        return answer;
    }

    public static void main(String[] args) {
        DailyTemperatures solver = new DailyTemperatures();
        int[] temperatures = {73, 74, 75, 71, 69, 72, 76, 73};
        int[] result = solver.dailyTemperatures(temperatures);
        for (int days : result) {
            System.out.print(days + " "); // Output: 1 1 4 2 1 1 0 0
        }
    }
}
```

---

## **🔹 Dry Run Example**

#### **Input:** `[73,74,75,71,69,72,76,73]`

**Step-by-step processing with Stack:**

```text
i = 0, temp = 73 → Push (index 0)
i = 1, temp = 74 → 74 > 73 → Pop(0), answer[0] = 1 → Push (1)
i = 2, temp = 75 → 75 > 74 → Pop(1), answer[1] = 1 → Push (2)
i = 3, temp = 71 → Push (3)
i = 4, temp = 69 → Push (4)
i = 5, temp = 72 → 72 > 69 → Pop(4), answer[4] = 1
                   72 > 71 → Pop(3), answer[3] = 2 → Push (5)
i = 6, temp = 76 → 76 > 72 → Pop(5), answer[5] = 1
                   76 > 75 → Pop(2), answer[2] = 4 → Push (6)
i = 7, temp = 73 → Push (7)
```

**Final `answer[]` after the loop:** `[1,1,4,2,1,1,0,0]`

---

## **🚀 Summary**

|Approach|Time Complexity|Space Complexity|Notes|
|---|---|---|---|
|**Brute Force**|**O(N²)**|**O(1)**|Too slow for large `N`|
|**Stack-Based**|**O(N)**|**O(N)** (Stack)|Efficient ✅|

- **Brute Force:** Scans forward for each day **(O(N²))**.
    
- **Stack Approach:** Uses a **monotonic decreasing stack** to process in **O(N)**.
    
- **Stack stores indices, not temperatures** → Reduces redundant scans.
    

🚀 **Final Verdict:** Stack-based **O(N)** approach is optimal and widely used in coding interviews!