### Problem Statement

Link: https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/?envType=study-plan-v2&envId=top-interview-150

### Brute Force Approach
1. Use hash set to keep unique elements
2. Copy them to input array

### Solution
```java
  
class RemoveDuplicatesFromSortedArrayUsingHashSet {  
  
  public static void main(String[] args) {  
    RemoveDuplicatesFromSortedArrayUsingHashSet obj = new RemoveDuplicatesFromSortedArrayUsingHashSet();  
    int[] arr = {0, 0, 1, 1, 1, 2, 2, 3, 3, 4};  
    int n = obj.removeDuplicates(arr);  
    for (int i = 0; i < n; i++) {  
      System.out.print(arr[i] + " ");  
    }  
  }  
  
  private int removeDuplicates(int[] arr) {  
    HashSet<Integer> set = new HashSet<>();  
    for (int num : arr) {  
      set.add(num);  
    }  
  
    Iterator<Integer> iterator = set.iterator();  
    for (int i = 0; i < set.size(); i++) {  
      arr[i] = iterator.next();  
    }  
    return set.size();  
  }  
}
```

### Complexity analysis
##### Time
Adding a number to hashset takes O(1)
Iteration for n elements to create hashset O(n)
Copy to array from hashset o(k = unique elements)

Overall O(n) + O(k <= n) = O(n)

##### Space
O(k <= n) = O(n)

### Optimal Approach
1. Keep a index pointer for nextUniqueElement
2. Every time an element is found to be different than the element before nextUniqueElement, place it at nextUniqueElement index and move this pointer ahead
3. 0th index is always unique, so start from 1

### Solution
```java
class RemoveDuplicatesFromSortedArrayInPlace {  
  
  public static void main(String[] args) {  
    RemoveDuplicatesFromSortedArrayInPlace obj = new RemoveDuplicatesFromSortedArrayInPlace();  
    int[] arr = {0, 0, 1, 1, 1, 2, 2, 3, 3, 4};  
    int n = obj.removeDuplicates(arr);  
    for (int i = 0; i < n; i++) {  
      System.out.print(arr[i] + " ");  
    }  
  }  
  
  private int removeDuplicates(int[] arr) {  
    int n = arr.length;  
    int allowedDuplicatesSize = 1;  
  
    if (n <= allowedDuplicatesSize) {  
      return n;  
    }  
  
    int nextUniqueElementIndex = allowedDuplicatesSize;  
  
    for (int i = allowedDuplicatesSize; i < n; i++) {  
      int currentElement = arr[i];  
      int previousElement = arr[nextUniqueElementIndex - allowedDuplicatesSize];  
  
      if (currentElement != previousElement) {  
        arr[nextUniqueElementIndex++] = currentElement;  
      }  
  
    }  
    return nextUniqueElementIndex;  
  }  
}
```

### Complexity analysis
##### Time
O(n)

##### Space
O(1)

### Attachments
![[Pasted image 20250121065940.png]]

### Tags
[[2 pointer]]
[[Hashing]]
[[Top 150 Leetcode]]
[[Arrays]]

### References