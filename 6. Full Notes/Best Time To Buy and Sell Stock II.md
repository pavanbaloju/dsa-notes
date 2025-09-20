### Problem Statement

Link: https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/?envType=study-plan-v2&envId=top-interview-150

For each index, we find multiple occasions where we can buy and sell
2. Like find those pairs of days, where one day you buy and other day we sell, when we sum the profits from all these pairs, we can the total profit
3. Each pair doesn't overlap but come in continous order in array
4. Here the thing is for each buy day, u can have multiple sell days and based on each sell day, you will have next buy days and then multiple sell days and so on
5. There is overlapping subproblems with in a single problem and optimal substructure
### Brute Force Approach
1. Generate all possible subsets of transactions, calculate the profit for each subset, and find the maximum profit.
2. Whenever there is a thing like all possible subsets or possibilities, it means 2^n possibilities will be there and this is an indication of backtracking and DP problem
3.  **Steps**:
	1. Use recursion or backtracking to generate all possible combinations of buy-sell pairs.
	2. For each combination, calculate the total profit.
	3. Track the maximum profit.

### Solution
```java
class BestTimeToBuyAndSell2BruteForce {  
  
  public static void main(String[] args) {  
    int[] prices = {7, 1, 5, 3, 6, 4};  
    System.out.println(maxProfit(prices));  
  }  
  
  // Time: O(2^n), Space: O(n)  
  public static int maxProfit(int[] prices) {  
    return maximizeProfitForDay(prices, 0);  
  }  
  
  private static int maximizeProfitForDay(int[] prices, int buyDay) {  
    if (buyDay >= prices.length) {  
      return 0;  
    }  
    int bestSellProfit = 0;  
    for (int sellDay = buyDay; sellDay < prices.length; sellDay++) {  
      int nextBuyDay = sellDay + 1;  
      int todaySellProfit = prices[sellDay] - prices[buyDay];  
      int maximumProfitIfWeSellToday = todaySellProfit + maximizeProfitForDay(prices, nextBuyDay);  
      bestSellProfit = Math.max(bestSellProfit, maximumProfitIfWeSellToday);  
    }  
    return bestSellProfit;  
  }  
}

```

### Complexity analysis
##### Time
O(4^n)
##### Space
O(1)

### Another Brute Force Approach
1. Backtracking

### Solution
```java
class BestTimeToBuyAndSell2Backtracking {  
  
  public static void main(String[] args) {  
    int[] prices = {7, 1, 5, 3, 6, 4};  
    System.out.println(maxProfit(prices));  
  }  
  
  // Time: O(2^n), Space: O(n)  
  public static int maxProfit(int[] prices) {  
    return maximizeProfit(prices, 0, false);  
  }  
  
  private static int maximizeProfit(int[] prices, int day, boolean holdingStock) {  
    if (day >= prices.length) {  
      return 0;  
    }  
    int todayPrice = prices[day];  
    int tomorrow = day + 1;  
  
    if (holdingStock) {  
      int sellToday = maximizeProfit(prices, tomorrow, false) + todayPrice;  
      int skipToday = maximizeProfit(prices, tomorrow, true);  
      return Math.max(sellToday, skipToday);  
    } else {  
      int buyToday = maximizeProfit(prices, tomorrow, true) - todayPrice;  
      int skipToday = maximizeProfit(prices, tomorrow, false);  
      return Math.max(buyToday, skipToday);  
    }  
  
  }  
}
```

### Complexity analysis
##### Time
O(2^n)

##### Space
O(1)

### Better Approach
1. Backtracking with memoization
2. Tabulation

### Solution
```java
  
class BestTimeToBuyAndSell2BacktrackingWithMemoization {  
  
  public static void main(String[] args) {  
    int[] prices = {7, 1, 5, 3, 6, 4};  
    System.out.println(maxProfit(prices));  
  }  
  
  // Time: O(n), Space: O(n)  
  public static int maxProfit(int[] prices) {  
    Integer[][] memo = new Integer[prices.length][2];  
    for (int i = 0; i < prices.length; i++) {  
      memo[i][0] = null;  
      memo[i][1] = null;  
    }  
    return maximizeProfit(prices, 0, false, memo);  
  }  
  
  private static int maximizeProfit(int[] prices, int day, boolean holdingStock, Integer[][] memo) {  
    if (day >= prices.length) {  
      return 0;  
    }  
  
    if (memo[day][holdingStock ? 1 : 0] != null) {  
      return memo[day][holdingStock ? 1 : 0];  
    }  
  
    int todayPrice = prices[day];  
    int tomorrow = day + 1;  
  
    if (holdingStock) {  
      int sellToday = maximizeProfit(prices, tomorrow, false, memo) + todayPrice;  
      int skipToday = maximizeProfit(prices, tomorrow, true, memo);  
      memo[day][1] = Math.max(sellToday, skipToday);  
      return memo[day][1];  
    } else {  
      int buyToday = maximizeProfit(prices, tomorrow, true, memo) - todayPrice;  
      int skipToday = maximizeProfit(prices, tomorrow, false, memo);  
      memo[day][0] = Math.max(buyToday, skipToday);  
      return memo[day][0];  
    }  
  }  
}  
  
class BestTimeToBuyAndSell2WithTabulation {  
  
  public static void main(String[] args) {  
    int[] prices = {7, 1, 5, 3, 6, 4};  
    System.out.println(maxProfit(prices));  
  }  
  
  // Time: O(n), Space: O(n)  
  public static int maxProfit(int[] prices) {  
    Integer[][] dp = new Integer[prices.length][2];  
    for (int i = 0; i < prices.length; i++) {  
      dp[i][0] = null;  
      dp[i][1] = null;  
    }  
    return maximizeProfit(prices, dp);  
  }  
  
  private static int maximizeProfit(int[] prices, Integer[][] dp) {  
  
    for (int day = prices.length - 1; day >= 0; day--) {  
  
      int todayPrice = prices[day];  
      int tomorrow = day + 1;  
  
      if (day == prices.length - 1) {  
        dp[day][0] = 0;  
        dp[day][1] = todayPrice;  
        continue;  
      }  
  
      int buyToday = dp[tomorrow][1] - todayPrice;  
      int skipToday = dp[tomorrow][0];  
      dp[day][0] = Math.max(buyToday, skipToday);  
  
      int sellToday = dp[tomorrow][0] + todayPrice;  
      int skipToday2 = dp[tomorrow][1];  
      dp[day][1] = Math.max(sellToday, skipToday2);  
    }  
    return dp[0][0];  
  }  
}
```

### Complexity analysis
##### Time
O(n)

##### Space
O(n)

### Optimal Approach by Greedy
1. Just but at low and set at high
2. For each day if we see the price is better than yesterday, we are making profit means like buying yesterday and selling today


### Solution
```java
class BestTimeToBuyAndSell2Better {  
  
  public static void main(String[] args) {  
    int[] prices = {7, 1, 5, 3, 6, 4};  
    System.out.println(maxProfit(prices));  
  }  
  
  // Time: O(n), Space: O(1)  
  public static int maxProfit(int[] prices) {  
    int profit = 0;  
    for (int day = 1; day < prices.length; day++) {  
  
      int todayPrice = prices[day];  
      int yesterdayPrice = prices[day - 1];  
  
      if (todayPrice > yesterdayPrice) {  
        profit += todayPrice - yesterdayPrice;  
      }  
    }  
    return profit;  
  }  
}
```

### Complexity analysis
##### Time
O(n)

##### Space
O(1)
### Optimal Approach By Tabulation
1. Optimized Tabulation

### Solution
```java
  
class BestTimeToBuyAndSell2WithTabulationOptimized {  
  
  public static void main(String[] args) {  
    int[] prices = {7, 1, 5, 3, 6, 4};  
    System.out.println(maxProfit(prices));  
  }  
  
  // Time: O(n), Space: O(1)  
  public static int maxProfit(int[] prices) {  
    int[] dpTomorrow = {0, prices[prices.length - 1]};  
    for (int day = prices.length - 2; day >= 0; day--) {  
  
      int todayPrice = prices[day];  
  
      int buyToday = dpTomorrow[1] - todayPrice;  
      int skipToday = dpTomorrow[0];  
      dpTomorrow[0] = Math.max(buyToday, skipToday);  
  
      int sellToday = dpTomorrow[0] + todayPrice;  
      int skipToday2 = dpTomorrow[1];  
      dpTomorrow[1] = Math.max(sellToday, skipToday2);  
    }  
    return dpTomorrow[0];  
  }  
}
```

### Complexity analysis
##### Time
O(n)

##### Space
O(n)
### Attachments
![[Pasted image 20250123072302.png]]

### Tags
[[Top 150 Leetcode]]
[[Arrays]]
[[Greedy]]
[[Dynamic Programming]]
[[Backtracking]]

### References
[[Best Time To Buy and Sell Stock]]