### Problem Statement

Link: https://leetcode.com/problems/majority-element/description/?envType=study-plan-v2&envId=top-interview-150

### Brute Force Approach
1. For each element, calculate count and if count > n / 2 return it

### Solution
```java
class MajorityElementBruteForce {  
  
  public static void main(String[] args) {  
    int[] nums = {2, 2, 1, 1, 1, 2, 2};  
    System.out.println(majorityElement(nums));  
  }  
  
  // O(n^2) time complexity  
  // O(1) space complexity  public static int majorityElement(int[] nums) {  
    int n = nums.length;  
  
    for (int currentElementIndex = 0; currentElementIndex < n; currentElementIndex++) {  
      int count = 0;  
      for (int countingIndex = 0; countingIndex < n; countingIndex++) {  
        if (nums[currentElementIndex] == nums[countingIndex]) {  
          count++;  
        }  
      }  
      if (count > n / 2) {  
        return nums[currentElementIndex];  
      }  
    }  
    return -1;  
  }  
}
```

### Complexity analysis
##### Time
O(n^2)

##### Space
O(1)

### Better Approach
1. Sort and count for elements in a single pass
2. When element changes, check if previous count > n/ 2 and return if yes

### Solution
```java
  
class MajorityElementSorting {  
  
  public static void main(String[] args) {  
    int[] nums = {2, 2, 1, 1, 1, 2, 2};  
    System.out.println(majorityElement(nums));  
  }  
  
  // O(nlogn) time complexity  
  // O(1) space complexity  public static int majorityElement(int[] nums) {  
    int n = nums.length;  
  
    Arrays.sort(nums);  
    int count = 1;  
    for (int i = 1; i < n; i++) {  
      if (nums[i] == nums[i - 1]) {  
        count++;  
      } else {  
        if (count > n / 2) {  
          return nums[i - 1];  
        }  
        count = 1;  
      }  
    }  
  
    // Check the last element  
    if (count > n / 2) {  
      return nums[n - 1];  
    }  
  
    return -1;  
  }  
}
```

### Complexity analysis
##### Time
O(n log(n))

##### Space
O(1)

### Better Approach
1. Use hashing to calculate frequency
2. When frequency reaches > n/ 2 return that element

### Solution
```java
  
class MajorityElementHashing {  
  
  public static void main(String[] args) {  
    int[] nums = {2, 2, 1, 1, 1, 2, 2};  
    System.out.println(majorityElement(nums));  
  }  
  
  // O(n) time complexity  
  // O(n) space complexity  public static int majorityElement(int[] nums) {  
    int n = nums.length;  
    HashMap<Integer, Integer> countMap = new HashMap<>();  
    for (int num : nums) {  
      countMap.put(num, countMap.getOrDefault(num, 0) + 1);  
      if (countMap.get(num) > n / 2) {  
        return num;  
      }  
    }  
  
    return -1;  
  }  
}
```

### Complexity analysis
##### Time
O(n)

##### Space
O(n)

### Optimal Approach
1. Moore's voting algorithm

### Solution
```java
class MajorityElementMooresVotingAlgorithm {  
  
  public static void main(String[] args) {  
    int[] nums = {2, 2, 1, 1, 1, 2, 2};  
    System.out.println(majorityElement(nums));  
  }  
  
  // O(n) time complexity  
  // O(1) space complexity  public static int majorityElement(int[] nums) {  
    int count = 0;  
    int candidate = 0;  
  
    for (int num : nums) {  
      if (count == 0) {  
        candidate = num;  
      }  
      if (num == candidate) {  
        count++;  
      } else {  
        count--;  
      }  
    }  
    return candidate;  
  }  
}
```

### Complexity analysis
##### Time
O(n)
##### Space
O(1)

### Attachments


### Tags
[[Top 150 Leetcode]]
[[Boyer Moore's Voting Algorithm]]
[[Arrays]]

### References