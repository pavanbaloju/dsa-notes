### Problem Statement

Link: https://leetcode.com/problems/merge-sorted-array/description/?envType=study-plan-v2&envId=top-interview-150

### Brute Force Approach
1. Copy all elements to nums1 and then sort nums1

### Solution
```java
class MergeSortedArraysBruteForce {  
  
  public static void main(String[] args) {  
    int[] nums1 = {1, 2, 3, 0, 0, 0};  
    int[] nums2 = {2, 5, 6};  
  
    merge(nums1, 3, nums2, 3);  
    System.out.println("------Merged Arrays by Brute Force-----");  
    Arrays.stream(nums1).forEach(System.out::println);  
  }  
  
  private static void merge(int[] nums1, int m, int[] nums2, int n) {  
    for (int num: nums2) {  
      nums1[m++] = num;  
    }  
    Arrays.sort(nums1);  
  }  
}
```

### Complexity analysis
##### Time
O((m+n)log(m+n))

##### Space
O(1)

### Better Approach
1. Take a new array with the size of both arrays
2. copy elements in increasing order into new array comparing elements from both arrays
3. once done, copy new array to nums1

### Solution
```java
class MergeSortedArraysBetter {  
  
  public static void main(String[] args) {  
    int[] nums1 = {1, 2, 3, 0, 0, 0};  
    int[] nums2 = {2, 5, 6};  
  
    merge(nums1, 3, nums2, 3);  
    System.out.println("------Merged Arrays by Better-----");  
    Arrays.stream(nums1).forEach(System.out::println);  
  }  
  
  private static void merge(int[] nums1, int m, int[] nums2, int n) {  
    int[] sorted = new int[m + n];  
    int i, j;  
    for (i = 0, j = 0; i < m && j < n;) {  
      if (nums1[i] <= nums2[j]) {  
        sorted[i + j] = nums1[i++];  
      } else {  
        sorted[i + j] = nums2[j++];  
      }  
    }  
  
    while (i < m) {  
      sorted[i + j] = nums1[i++];  
    }  
    while (j < n) {  
      sorted[i + j] = nums2[j++];  
    }  
  
    for (int k = 0; k < m + n; k++) {  
      nums1[k] = sorted[k];  
    }  
  }  
}
```

### Complexity analysis
##### Time
O(m + n)

##### Space
O(m + n)

### Optimal Approach
1. Copy elements to the back of nums1 in decreasing order by comparing elements of both arrays
2. copy any left over elements in nums2 to empty slots in nums1

### Solution
```java
class MergeSortedArraysOptimal {  
  
  public static void main(String[] args) {  
    int[] nums1 = {1, 2, 3, 0, 0, 0};  
    int[] nums2 = {2, 5, 6};  
  
    merge(nums1, 3, nums2, 3);  
    System.out.println("------Merged Arrays Optimal-----");  
    Arrays.stream(nums1).forEach(System.out::println);  
  
    nums1 = new int[]{0, 0, 0};  
    nums2 = new int[]{2, 5, 6};  
  
    merge(nums1, 0, nums2, 3);  
    System.out.println("------Merged Arrays Optimal-----");  
    Arrays.stream(nums1).forEach(System.out::println);  
  
    nums1 = new int[]{2, 5, 6};  
    nums2 = new int[]{};  
  
    merge(nums1, 3, nums2, 0);  
    System.out.println("------Merged Arrays Optimal-----");  
    Arrays.stream(nums1).forEach(System.out::println);  
  }  
  
  private static void merge(int[] nums1, int m, int[] nums2, int n) {  
    int k = m + n - 1;  
    m--;  
    n--;  
    while (m >= 0 && n >= 0) {  
      if (nums1[m] >= nums2[n]) {  
        nums1[k--] = nums1[m--];  
      } else {  
        nums1[k--] = nums2[n--];  
      }  
    }  
  
    while (n >= 0) {  
      nums1[k--] = nums2[n--];  
    }  
  }  
}
```

### Complexity analysis
##### Time
O(m + n)

##### Space
O(1)

### Attachments
![[Pasted image 20250116082421.png]]

### Tags
[[Top 150 Leetcode]]
[[Arrays]]

### References