### Insertion Sort

In this assignment, you implement in-place insertion sort. 
The method insertionSort takes as input an array of integers and returns a sorted array in increasing order. 
Your implementation should be the insertion sort algorithm.

```java
class Solution {
  /**
   * @param elements
   *     - array of integers to be sorted.
   */
  public static void insertionSort(int[] elements) {
    for (int i = 1; i < elements.length; ++i) { 
            int key = elements[i]; 
            int j = i - 1; 
            while (j >= 0 && elements[j] > key) { 
                elements[j + 1] = elements[j]; 
                j = j - 1; 
            } 
            elements[j + 1] = key; 
        } 
  }
}
```
