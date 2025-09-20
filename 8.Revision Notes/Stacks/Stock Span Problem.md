## **Stock Span Problem (LeetCode 901: Online Stock Span)**

### **Problem Statement**

The **Stock Span Problem** is a financial problem where we calculate the **span of stock prices** for each day.  
The span of a stock's price for a given day is **the number of consecutive days (including today) the price has been less than or equal to today’s price**.

### **Example**

```java
Input:  prices = [100, 80, 60, 70, 60, 75, 85]
Output: [1, 1, 1, 2, 1, 4, 6]
```

#### **Explanation**

For each price, we count how many previous days (including today) had a price **≤ today's price**:

```
Day 1: 100 → span = 1
Day 2:  80 → span = 1
Day 3:  60 → span = 1
Day 4:  70 → span = 2 (70, 60)
Day 5:  60 → span = 1
Day 6:  75 → span = 4 (75, 60, 70, 60)
Day 7:  85 → span = 6 (85, 75, 60, 70, 60, 80)
```

---

## **🔹 Approach 1: Brute Force (O(N²))**

For each day `i`, we look backward to count **how many consecutive** days had prices **≤ price[i]**.

### **Code (Brute Force)**

```java
public int[] calculateSpan(int[] prices) {
    int n = prices.length;
    int[] span = new int[n];

    for (int i = 0; i < n; i++) {
        span[i] = 1; // Minimum span is 1 (itself)
        for (int j = i - 1; j >= 0 && prices[j] <= prices[i]; j--) {
            span[i]++;
        }
    }

    return span;
}
```

🔴 **Time Complexity:** **O(N²)** (Nested loops) → Inefficient!

---

## **🔹 Approach 2: Monotonic Stack (O(N))**

### **Key Idea**

Instead of looking back **brute force**, we use a **monotonic decreasing stack** to efficiently find the nearest **greater price to the left**.

1. **Use a stack** to store indices.
    
2. **Maintain a decreasing order in the stack** (top holds the most recent higher price).
    
3. **If the current price is higher than stack top**, pop until we find a higher price.
    
4. **Calculate span** using the popped index.
    

### **Code (Optimal)**

```java
import java.util.Stack;

public class StockSpan {
    public int[] calculateSpan(int[] prices) {
        int n = prices.length;
        int[] span = new int[n];
        Stack<Integer> stack = new Stack<>();

        for (int i = 0; i < n; i++) {
            // Pop smaller or equal elements
            while (!stack.isEmpty() && prices[stack.peek()] <= prices[i]) {
                stack.pop();
            }

            // Compute span
            span[i] = stack.isEmpty() ? (i + 1) : (i - stack.peek());

            // Push current index
            stack.push(i);
        }

        return span;
    }

    public static void main(String[] args) {
        StockSpan stockSpan = new StockSpan();
        int[] prices = {100, 80, 60, 70, 60, 75, 85};
        int[] spans = stockSpan.calculateSpan(prices);

        for (int s : spans) {
            System.out.print(s + " ");
        }
        // Output: 1 1 1 2 1 4 6
    }
}
```

---

## **🔹 Dry Run**

**Input:** `prices = [100, 80, 60, 70, 60, 75, 85]`

|Day|Price|Stack (Indices)|Popped Elements|Span Calculation|
|---|---|---|---|---|
|1|100|`[0]`|None|`1` (100 itself)|
|2|80|`[0, 1]`|None|`1`|
|3|60|`[0, 1, 2]`|None|`1`|
|4|70|`[0, 1]`|`[2]`|`i - stack.top = 3 - 1 = 2`|
|5|60|`[0, 1, 4]`|None|`1`|
|6|75|`[0, 1]`|`[4, 3, 1]`|`i - stack.top = 5 - 1 = 4`|
|7|85|`[0]`|`[5, 1, 0]`|`i - stack.top = 6 - 0 = 6`|

---

## **🚀 Summary**

|Approach|Time Complexity|Space Complexity|Notes|
|---|---|---|---|
|**Brute Force**|**O(N²)**|**O(1)**|Slow ❌|
|**Stack-Based**|**O(N)**|**O(N)**|Best ✅|

✔ **Stack-Based Solution** is the best for interviews because it efficiently computes **previous greater elements** in **O(N)** time.