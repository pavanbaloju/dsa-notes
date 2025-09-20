### Problem Statement

Link: https://leetcode.com/problems/best-time-to-buy-and-sell-stock/?envType=study-plan-v2&envId=top-interview-150

### Brute Force Approach
1. Iterate through all pairs of days to calculate the profit and track the maximum profit.
2. Steps:
    1. Use a nested loop to consider every pair of days (i,j) such that j >i
    2. Calculate profit for each pair: profit = prices[j] − prices[i].
    3. Update the maximum profit if profit > maxProfit.

### Solution
```java
class BestTimeToBuyAndSellBruteForce {  
  
  public static void main(String[] args) {  
    int[] prices = {7, 1, 5, 3, 6, 4};  
    System.out.println(maxProfit(prices));  
  }  
  
  // Time Complexity: O(n^2)  
  // Space Complexity: O(1)  public static int maxProfit(int[] prices) {  
    int maxProfit = 0;  
    int days = prices.length;  
    for (int buyIndex = 0; buyIndex < days; buyIndex++) {  
      for (int sellIndex = buyIndex + 1; sellIndex < days; sellIndex++) {  
        maxProfit = Math.max(maxProfit, prices[sellIndex] - prices[buyIndex]);  
      }  
    }  
    return maxProfit;  
  }  
}
```

### Complexity analysis
##### Time
O(n^2)
##### Space
O(1)

### Better Approach
1. For each day, buy if we find a price than better previous buy price
2. sell if we find a price greater than buy price keeping track of best sell price so far

### Solution
```java
class BestTimeToBuyAndSellGreedy {  
  
  public static void main(String[] args) {  
    int[] prices = {7, 1, 5, 3, 6, 4};  
    System.out.println(maxProfit(prices));  
  }  
  
  // Time Complexity: O(n)  
  // Space Complexity: O(1)  public static int maxProfit(int[] prices) {  
    int bestBuyPrice = Integer.MAX_VALUE;  
    int bestSellProfit = 0;  
  
    for (int todayPrice: prices) {  
      if (todayPrice < bestBuyPrice) {  
        bestBuyPrice = todayPrice;  
      }  
      else {  
        bestSellProfit = Math.max(bestSellProfit, todayPrice - bestBuyPrice);  
      }  
    }  
    return bestSellProfit;  
  }  
}
```

### Complexity analysis
##### Time
O(n)

##### Space
O(1)

### Optimal Approach
1. Use a dynamic programming approach to store intermediate results, such as the minimum price and maximum profit up to each day
2. Steps
	1. Define dp[i] as the maximum profit achievable up to the i-th day
	2. Transition relation:
		1. dp[i] =max⁡(dp[i−1], prices[i] − minPrice)

### Solution
```java
class BestTimeToBuyAndSellDynamicProgramming {  
  
  public static void main(String[] args) {  
    int[] prices = {7, 1, 5, 3, 6, 4};  
    System.out.println(maxProfit(prices));  
  }  
  
  // Time Complexity: O(n)  
  // Space Complexity: O(1)  
  public static int maxProfit(int[] prices) {  
    int days = prices.length;  
    int minPrice = prices[0];  
    int maxProfit = 0;  
  
    for (int i = 1; i < days; i++) {  
      minPrice = Math.min(minPrice, prices[i]);  
      maxProfit = Math.max(maxProfit, prices[i] - minPrice);  
    }  
    return maxProfit;  
  }  
}
```

### Complexity analysis
##### Time
O(n)

##### Space
O(1)

### Attachments
![[Pasted image 20250121080148.png]]

### Tags
[[Top 150 Leetcode]]
[[Arrays]]
[[Greedy]]
[[Dynamic Programming]]
[[Backtracking]]
### References