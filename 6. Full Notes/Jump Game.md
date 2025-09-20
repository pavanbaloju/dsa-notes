### Problem Statement

Link: https://leetcode.com/problems/jump-game/?envType=study-plan-v2&envId=top-interview-150

### Brute Force Approach
1. Try all possible jumps from each place and check if are able to reach end

### Solution
```java
class JumpGameBruteForce {  
  
  public static void main(String[] args) {  
    int[] nums = {2, 3, 1, 1, 4};  
    System.out.println(canJump(nums));  
  }  
  
  // Time Complexity: O(2^n)  
  // Space Complexity: O(n)  public static boolean canJump(int[] nums) {  
    return canReachEnd(0, nums);  
  }  
  
  private static boolean canReachEnd(int pos, int[] nums) {  
    if (pos >= nums.length - 1) {  
      return true;  
    }  
  
    int furthestJump = Math.min(pos + nums[pos], nums.length - 1);  
  
    for (int nextPos = pos + 1; nextPos <= furthestJump; nextPos++) {  
      if (canReachEnd(nextPos, nums)) {  
        return true;  
      }  
    }  
    return false;  
  }  
}
```

### Complexity analysis
##### Time
O(n^n)

##### Space
O(1)

### Better Approach
1. Memoization and Tabulation

### Solution
```java
class JumpGameBackTrackingMemoization {  
  
  public static void main(String[] args) {  
    int[] nums = {2, 3, 1, 1, 4};  
    System.out.println(canJump(nums));  
  }  
  
  // Time Complexity: O(n^2)  
  // Space Complexity: O(n)  public static boolean canJump(int[] nums) {  
    int[] memo = new int[nums.length];  
    memo[nums.length - 1] = 1;  
    return canReachEnd(0, nums, memo);  
  }  
  
  private static boolean canReachEnd(int pos, int[] nums, int[] memo) {  
    if (memo[pos] != 0) {  
      return memo[pos] == 1;  
    }  
  
    int furthestJump = Math.min(pos + nums[pos], nums.length - 1);  
    for (int nextPos = pos + 1; nextPos <= furthestJump; nextPos++) {  
      if (canReachEnd(nextPos, nums, memo)) {  
        memo[pos] = 1;  
        return true;  
      }  
    }  
    memo[pos] = -1;  
    return false;  
  }  
}  
  
class JumpGameTabulation {  
  
  public static void main(String[] args) {  
    int[] nums = {2, 3, 1, 1, 4};  
    System.out.println(canJump(nums));  
  }  
  
  // Time Complexity: O(n^2)  
  // Space Complexity: O(n)  public static boolean canJump(int[] nums) {  
    boolean[] dp = new boolean[nums.length];  
    dp[nums.length - 1] = true; // The last index is always reachable.  
  
    for (int i = nums.length - 2; i >= 0; i--) {  
      int maxJump = Math.min(i + nums[i], nums.length - 1);  
      for (int j = i + 1; j <= maxJump; j++) {  
        if (dp[j]) { // If we can reach the last index from this index.  
          dp[i] = true; // Mark this index as reachable.  
          break;  
        }  
      }  
    }  
    return dp[0]; // Can we reach the last index from the first index?  
  }  
  
}
```

### Complexity analysis
##### Time
O(n^2)

##### Space
O(1)

### Optimal Approach
1. Greedy Approach

### Solution
```java
  
class JumpGameGreedy1 {  
  
  public static void main(String[] args) {  
    int[] nums = {2, 3, 1, 1, 4};  
    System.out.println(canJump(nums)); // Output: true  
  }  
  
  // Time Complexity: O(n)  
  // Space Complexity: O(1)  public static boolean canJump(int[] nums) {  
    int destination = nums.length - 1; // Start with the last index as reachable.  
  
    for (int currentPos = nums.length - 2; currentPos >= 0; currentPos--) {  
  
      int distanceReachable = currentPos + nums[currentPos];  
      if (distanceReachable >= destination) {  
        // If we can jump from index `currentPos` to `destination`  
        destination = currentPos; // Update destination to current index  
      }  
  
    }  
  
    // Check if the first index can reach the last index  
    return destination == 0;  
  }  
}  
  
  
class JumpGameGreedy {  
  
  public static void main(String[] args) {  
    int[] nums = {2, 3, 1, 1, 4};  
    System.out.println(canJump(nums));  
  }  
  
  public static boolean canJump(int[] nums) {  
    int distanceReachable = 0; // The distanceReachable index we can reach.  
    for (int currentPosition = 0; currentPosition < nums.length; currentPosition++) {  
      if (currentPosition  > distanceReachable) {  
        return false; // Current index is not reachable.  
      }  
      distanceReachable = Math.max(distanceReachable, currentPosition + nums[currentPosition]);  
    }  
    return distanceReachable >= nums.length - 1; // Can the distanceReachable index reach the last index?  
  }  
}
```

### Complexity analysis
##### Time
O(n)

##### Space
O(1)

### Attachments
![[Pasted image 20250124070948.png]]

### Tags
[[Top 150 Leetcode]]
[[Arrays]]
[[Greedy]]
[[Dynamic Programming]]
[[Backtracking]]
### References