Implement the function sumElementsUpTo(int[] arr, int n) that calculates the sum of all elements in the array up to (and including) the nth element.
You can assume 0 <= n < arr.length

Solve this problem with an iterative approach.

```java
class Solution {

  /**
   * Returns the sum of all elements in the array up to (and including) the `n`th element
   *
   * @param arr the array of integers that needs to be summed
   * @param n the index of the last item to consider
   */
  public static int sumElementsUpTo(int[] arr, int n) {
    int result = 0;
    for(int i =0; i <= n; i++) {
      result += arr[i];
    }
    return result;
  }
}
```
