Implement the function sumElementsUpTo(int[] arr, int n) that calculates the sum of all elements in the array up to (and including) the nth element.
You can assume 0 <= n < arr.length

Solve this problem with the recursive approach. You are allowed to make use of a helper method.

```java
class Solution {

  /**
   * Returns the sum of all elements in the array up to (and including) the `n`th element
   *
   * @param arr the array of integers that needs to be summed
   * @param n the index of the last item to consider
   */
  public static int sumElementsUpTo(int[] arr, int n) {
    if(n < 0) return 0;
    return arr[n] + sumElementsUpTo(arr, n-1);
  }
}

```
