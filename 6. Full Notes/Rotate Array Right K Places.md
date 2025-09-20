### Problem Statement

Link:

### Brute Force Approach
1. Rotate the array kkk times by shifting elements one position to the right in each iteration.
2. Repeat k times:
	- Store the last element in a temporary variable.
	- Shift all other elements one position to the right.
	- Place the stored element at the beginning.

### Solution
```java
class RotateArrayBruteForce {  
  
  public static void main(String[] args) {  
    RotateArrayBruteForce obj = new RotateArrayBruteForce();  
    int[] arr = {1, 2, 3, 4, 5, 6, 7};  
    int k = 3;  
    obj.rotate(arr, k);  
    for (int i : arr) {  
      System.out.print(i + " ");  
    }  
  }  
  
  // Time Complexity: O(n*k)  
  // Space Complexity: O(1)  public void rotate(int[] arr, int k) {  
    int n = arr.length;  
    k = k % n;  
  
    for (int noOfPlaces = 0; noOfPlaces < k; noOfPlaces++) {  
      int last = arr[n - 1];  
      for (int i = n - 1; i > 0; i--) {  
        arr[i] = arr[i - 1];  
      }  
      arr[0] = last;  
    }  
  }  
}
```

### Complexity analysis
##### Time
O(n x k)
##### Space
O(1)

### Better Approach
1. Use an extra array to store the rotated result.
	1. Create a new array of the same size as the input.
	2. Place each element at its new position: 
		1. new_index = (i + k) % n
2. Copy the new array back to the original array.

### Solution
```java
class RotateArrayExtraArray {  
  
  public static void main(String[] args) {  
    RotateArrayExtraArray obj = new RotateArrayExtraArray();  
    int[] arr = {1, 2, 3, 4, 5, 6, 7};  
    int k = 3;  
    obj.rotate(arr, k);  
    for (int i : arr) {  
      System.out.print(i + " ");  
    }  
  }  
  
  // Time Complexity: O(n)  
  // Space Complexity: O(n)  public void rotate(int[] arr, int k) {  
    int n = arr.length;  
    k = k % n;  
    int[] temp = new int[n];  
  
    for (int i = 0; i < n; i++) {  
      temp[(i + k) % n] = arr[i];  
    }  
  
    for (int i = 0; i < n; i++) {  
      arr[i] = temp[i];  
    }  
  }  
}
```

### Complexity analysis
##### Time
O(n)
##### Space
O(n)

### Optimal Approach
1. Reverse the entire array.
2. Reverse the first k elements.
3. Reverse the remaining n−k elements.

### Solution
```java
class RotateArrayByReversing {  
  
  public static void main(String[] args) {  
    RotateArrayByReversing obj = new RotateArrayByReversing();  
    int[] arr = {1, 2, 3, 4, 5, 6, 7};  
    int k = 3;  
    obj.rotate(arr, k);  
    for (int i : arr) {  
      System.out.print(i + " ");  
    }  
  }  
  
  // Time Complexity: O(n)  
  // Space Complexity: O(1)  public void rotate(int[] arr, int k) {  
    int n = arr.length;  
    k = k % n;  
  
    // Reverse the whole array  
    reverse(arr, 0, n - 1);  
  
    // Reverse the first k elements  
    reverse(arr, 0, k - 1);  
  
    // Reverse the last n - k elements  
    reverse(arr, k, n - 1);  
  }  
  
  private void reverse(int[] nums, int start, int end) {  
    while (start < end) {  
	  // swap
      int temp = nums[start];  
      nums[start] = nums[end];  
      nums[end] = temp;  
  
      start++;  
      end--;  
    }  
  }  
  
}
```

### Complexity analysis
##### Time
O(n)

##### Space
O(1)

### Attachments
![[Pasted image 20250121070006.png]]

### Tags
[[array rotations]]
[[Reverse array]]
[[Top 150 Leetcode]]
[[Arrays]]

### References