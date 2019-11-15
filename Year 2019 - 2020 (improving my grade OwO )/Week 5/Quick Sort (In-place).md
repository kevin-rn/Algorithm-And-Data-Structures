### Quick Sort (In-place) [not in the new version]
In this assignment, you have to implement in-place quicksort. A basic definition of this sorting algorithm is given as:

    Select a pivot.
    Partition the array into two, one part larger than pivot one part smaller.
    Repeat above on two partitions.
    Merge small | pivot | large

See:https://en.wikipedia.org/wiki/Quicksort

```java
class Solution {
  /**
   * @param elements
   *     Array of integers to be sorted.
   */
  public static void quickSort(int[] elements) {
    if(elements.length <= 1) return;
    int l =0, r=0, pivot = elements[elements.length-1];
    
    for(int i = 0; i<elements.length-1; i++) {
      if(elements[i] <= pivot) l++;
      else r++;
    }
    
    int[] left = new int[l];
    int[] right = new int[r];
    l=0;
    r=0;
    for(int i = 0; i<elements.length-1; i++) {
      if(elements[i] <= pivot) left[l++] = elements[i];
      else right[r++] = elements[i];
    }
    
    quickSort(left);
    quickSort(right);
    
    for(int i=0; i<elements.length; i++){
      if(i < l) elements[i] = left[i];
      else if(i == l) elements[i] = pivot;
      else elements[i] = right[i-left.length-1];
    }
  }
}
```
