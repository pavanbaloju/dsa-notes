## **Binary Search on Answer (Optimization Problems) – A Universal Pattern**

### **🔹 What is "Binary Search on Answer"?**

Unlike traditional **index-based** binary search (where you search for a target element), this technique is used to **find the optimal numerical value** that satisfies a given constraint.

This pattern is commonly used in problems that ask for:

- **The minimum feasible value** (e.g., minimum speed, capacity, or time)
    
- **The maximum feasible value** (e.g., maximum length, minimum cost, or maximum sum)
    

Instead of searching for an **exact element in an array**, we are searching for an **optimal numerical value within a defined range**.

---

## **🔹 Common Problems That Follow This Pattern**

- **Leetcode 875 – Koko Eating Bananas** (Find minimum speed to eat all bananas in `H` hours)
    
- **Leetcode 1011 – Capacity to Ship Packages Within D Days** (Find minimum ship capacity)
    
- **Leetcode 410 – Split Array Largest Sum** (Minimize the largest sum in `k` partitions)
    
- **Leetcode 1482 – Minimum Number of Days to Make m Bouquets** (Find the minimum number of days required)
    
- **Leetcode 1552 – Magnetic Force Between Two Balls** (Maximize minimum distance between balls)
    
- **Leetcode 1201 – Ugly Number III** (Find the nth ugly number using LCM)
    
- **Leetcode 2226 – Maximum Candies Allocated to k Children** (Maximize the number of candies per child)
    

---

## **🔹 Steps to Solve Any "Binary Search on Answer" Problem**

### **1️⃣ Define the Search Space**

- The **smallest possible answer** (`low`)
    
- The **largest possible answer** (`high`)
    
- Example: If searching for **minimum capacity**, `low = max(arr)`, `high = sum(arr)`.
    

### **2️⃣ Apply Binary Search on This Range**

- Compute `mid = (low + high) / 2` as the potential answer.
    
- Check if `mid` is a **valid solution** using a helper function.
    

### **3️⃣ Implement the Feasibility Function (`isValid(mid)`)**

- This function checks if a given `mid` value satisfies the problem constraints.
    
- If `mid` is valid, we **try for a better (smaller) answer**.
    
- If `mid` is **not valid**, we **increase `mid` to search for a feasible solution**.
    

### **4️⃣ Adjust `low` and `high` Based on the Feasibility Check**

- If `mid` is **valid**, we **move `high = mid`** to search for a smaller feasible value.
    
- If `mid` is **not valid**, we **move `low = mid + 1`** to increase the possible answer.
    

### **5️⃣ Return the First Feasible Value**

- The search stops when `low == high`, which is the **minimum/maximum feasible answer**.
    

---

## **🔹 Intuition Behind the Pattern**

This approach works when:

1. The **answer lies in a numerical range**.
    
2. If a solution `X` is **valid**, then all `X' > X` (or `< X`) may also be valid.
    
3. A **monotonic relationship** exists → As we increase/decrease `mid`, the result transitions from **invalid to valid** (or vice versa).
    

---

## **🔹 Example Walkthrough**

### **Example: Leetcode 875 – Koko Eating Bananas**

#### **Problem Statement:**

Koko can eat bananas at `K` bananas/hour. Given piles of bananas and `H` hours, find the **minimum speed `K`** such that she finishes all piles.

#### **Step 1: Define the Search Space**

- Minimum speed (`low`) = `1` (She can eat at least 1 banana/hour).
    
- Maximum speed (`high`) = `max(piles)` (Eating the largest pile in one hour).
    

#### **Step 2: Implement Binary Search on Answer**

```java
public int minEatingSpeed(int[] piles, int h) {
    int low = 1, high = Arrays.stream(piles).max().getAsInt();

    while (low < high) {
        int mid = low + (high - low) / 2;
        if (canFinish(piles, h, mid)) {
            high = mid; // Try a smaller speed
        } else {
            low = mid + 1;
        }
    }
    return low;
}
```

#### **Step 3: Implement the Feasibility Function**

```java
private boolean canFinish(int[] piles, int h, int speed) {
    int hours = 0;
    for (int pile : piles) {
        hours += Math.ceil((double) pile / speed);
    }
    return hours <= h;
}
```

---

## **🔹 Summary**

|Step|Explanation|
|---|---|
|**1️⃣ Define the search space**|Choose `low` and `high` based on problem constraints.|
|**2️⃣ Apply binary search on this range**|Find `mid` and check if it's feasible.|
|**3️⃣ Implement the feasibility function (`isValid`)**|Check if `mid` satisfies constraints.|
|**4️⃣ Adjust `low` and `high`**|If feasible, try a smaller value (`high = mid`). If not, increase (`low = mid + 1`).|
|**5️⃣ Return the optimal value**|When `low == high`, return the result.|

By following this approach, you can efficiently solve **Binary Search on Answer problems**! 🚀