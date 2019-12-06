Implement the merge sort algorithm. A definition of merge sort is given as:

    If the list contains 0 or 1 items, the list is sorted. The algorithm terminates.
    Split the list in 2 parts.
    Recursively sort the 2 sublists.
    Merge the 2 now sorted sublists in linear time.

Merge sort can be done both in-place and not-in-place. For this assignment you will create a not-in-place implementation.

A visualization of merge sort on https://en.wikipedia.org/wiki/Merge_sort

```java
import java.util.*;

class Solution {

  /**
   * Sorts an array of integers in ascending order. This operation is not-in-place.
   *
   * @param arr the array of integers that needs to be sorted in ascending order.
   */
  public static int[] mergeSort(int[] arr) {
    if (arr.length <= 1)
      return arr;
    int m = arr.length / 2;
    int[] left = Arrays.copyOfRange(arr, 0, m);
    int[] right = Arrays.copyOfRange(arr, m, arr.length);
    left = mergeSort(left);
    right = mergeSort(right);
    return merge(left, right);
  }

  private static int[] merge(int[] a, int[] b) {
    int[] res = new int[a.length + b.length];
    int i = 0;
    int j = 0;
    int r = 0;
    while (i < a.length && j < b.length) {
      if (a[i] < b[j])
        res[r++] = a[i++];
      else
        res[r++] = b[j++];
    }
    while (i < a.length) res[r++] = a[i++];
    while (j < b.length) res[r++] = b[j++];
    return res;
  }
}
```
