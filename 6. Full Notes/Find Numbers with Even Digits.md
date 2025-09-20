### Problem Statement

Link: https://leetcode.com/problems/find-numbers-with-even-number-of-digits/description/

### Brute Force Approach
1. For every number, count number of digits using division operator
2. Increment result when found a number with even digits

### Solution
```java
public class FindEvenDigitNumbers {

    public static int findNumbersWithDivision(int[] nums) {
        int count = 0;

        for (int num : nums) {
            int digitCount = 0;
            while (num > 0) {
                num /= 10;
                digitCount++;
            }

            if (digitCount % 2 == 0) {
                count++;
            }
        }

        return count;
    }

    public static void main(String[] args) {
        int[] nums = {12, 345, 2, 6, 7896};
        System.out.println("Count (Division): " +findNumbersWithDivision(nums));
    }
}

```

### Complexity analysis
Time : O(n x log (max integer))
Space: O(1)

### Better Approach

Number of digits in a number can be found by `Floor(Log(number)) + 1`

### Solution
```java
public class FindEvenDigitNumbers {

    public static int findNumbersWithLog(int[] nums) {
        int count = 0;

        for (int num : nums) {
            int digitCount = (int) Math.log10(num) + 1;
            if (digitCount % 2 == 0) {
                count++;
            }
        }

        return count;
    }

    public static void main(String[] args) {
        int[] nums = {12, 345, 2, 6, 7896};
        System.out.println("Count (Log): " + findNumbersWithLog(nums));
    }
}
```

### Complexity analysis
Time : O(n x log (max integer))
Space: O(1)

### Optimal Approach
Just by observing the input range, simply using if-else, we can get the number of even digit numbers

### Solution
```java
public class FindEvenDigitNumbers {

    public static int findNumbersWithConstraints(int[] nums) {
        int count = 0;

        for (int num : nums) {
            // Check if the number falls in ranges of even-digit numbers
            if ((num >= 10 && num < 100) || 
                (num >= 1000 && num < 10000) || 
                (num >= 100000 && num < 1000000)) {
                count++;
            }
        }

        return count;
    }

    public static void main(String[] args) {
        int[] nums = {12, 345, 2, 6, 7896};
        System.out.println("Count (Constraints): " + findNumbersWithConstraints(nums)); // Output: 2
    }
}

```

### Complexity analysis
Time : O(n)
Space: O(1)

### Attachments
![[Pasted image 20250112204923.png]]


### Tags
[[Arrays]] [[Maths]]
