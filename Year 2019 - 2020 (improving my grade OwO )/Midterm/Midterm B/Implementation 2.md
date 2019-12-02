In this assignment, you implement merge sort. The method mergeSort takes as input an array of integers and sorts the array in increasing order. Your implementation should be the merge sort algorithm.

Your implementation of merge sort does not need to be in-place.

IMPORTANT: Your code will be manually checked to see if you have actually implemented the merge sort algorithm.

    If you have used a sorting algorithm from the Java library, your grade will be overridden to 1.
    If you have implemented another sorting algorithm, you will get a score of 0.

```java
class Solution {
  /**
   * Takes an array and sorts it in an ascending order.
   * This has to be done by using merge sort.
   *
   * If the array is null, the metod should stop.
   *
   * @param arr
   *     - the array that needs to be sorted.
   */
  public static void mergeSort(int[] arr) {
    if(arr == null || arr.length <= 1) return;
    int size = arr.length/2;
    int[] left = new int[size];
    for(int i=0; i<size; i++) left[i] = arr[i];
    int[] right = new int[arr.length - size];
    for(int i = size; i<arr.length; i++) right[i-size] = arr[i];
    
    mergeSort(left);
    mergeSort(right);
    
    int l= 0, r= 0;
    for(int i= 0; i < arr.length; i++){
      if (l >= left.length) arr[i]= right[r++];
      else if (r >= right.length) arr[i]= left[l++];
      else if (left[l] <= right[r]) arr[i]= left[l++];
      else arr[i]= right[r++];
    }
  }
}
```
