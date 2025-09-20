### Problem Statement

Link: https://leetcode.com/problems/max-consecutive-ones/description/

### Brute Force Approach
- For every index, calculate the max consecutive ones
- To calculate the max consecutive ones, iterate through the whole array for every index and increment on seeing a 1 and end when encountered a 0
- While moving to next index, update the result with max consecutive ones so far

### Solution
```java
public class MaxConsecutiveOnes {

    public static int findMaxConsecutiveOnes(int[] nums) {
        int maxCount = 0; // To store the maximum count of consecutive ones

        for (int i = 0; i < nums.length; i++) {
            int count = 0; // To count consecutive ones starting from index i
            // Count consecutive ones from the current position
            for (int j = i; j < nums.length && nums[j] == 1; j++) {
                count++;
            }
            // Update the maximum count
            maxCount = Math.max(maxCount, count);
        }
        return maxCount;
    }

    public static void main(String[] args) {
        int[] nums = {1, 0, 1, 1, 1, 0, 0 , 1, 1};
        int maxConsecutiveOnes = findMaxConsecutiveOnes(nums);
        System.out.println("Maximum Consecutive Ones: " + maxConsecutiveOnes);
    }
}
```

### Complexity analysis

Time : O(n2)
Space: O(1)


### Better Approach

- For every index, keep track of current max consecutive ones and final max 
- If 1 is encountered, update the current max and final max
- If 0 is encountered, reset the current max

### Solution

```java
public class MaxConsecutiveOnes {

    public static int findMaxConsecutiveOnes(int[] nums) {
        int maxCount = 0; // Stores the maximum number of consecutive ones
        int currentCount = 0; // Tracks the current streak of ones

        for (int num : nums) {
            if (num == 1) {
                // Increment the current streak
                currentCount++;
                // Update maxCount if currentCount exceeds it
                maxCount = Math.max(maxCount, currentCount);
            } else {
                // Reset currentCount to 0 when a 0 is encountered
                currentCount = 0;
            }
        }

        return maxCount;
    }

    public static void main(String[] args) {
        int[] nums = {1, 1, 0, 1, 1, 1};

        System.out.println("Maximum Consecutive Ones: " + findMaxConsecutiveOnes(nums));
    }
}

```

### ### Complexity analysis

Time : O(n)
Space: O(1)
### Attachments

![[Pasted image 20250112195944.png]]
### Tags
[[Arrays]]
