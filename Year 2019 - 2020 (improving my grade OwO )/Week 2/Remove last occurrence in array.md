
Write a Java method removeLastOccurrence(int x, int[] arr), which removes the last occurrence of a given integer element x from a given array of integer elements arr.

The method should return a new array containing all elements in the given array arr except for the last occurrence of element x. The remaining elements should appear in the same order in the input and the returned arrays.

The code on the right shows you a code framework in which the implementation of one static method is still missing. Provide this implementation and check that it is correct by either writing more tests yourself or using the provided tests and specification tests.



```java
class Solution {
  /**
   * Takes the array and the last occurring element x,
   * shifting the rest of the elements left. I.e.
   * [1, 4, 7, 9], with x=7 would result in:
   * [1, 4, 9].
   *
   * @param x
   *     the entry to remove from the array
   * @param arr
   *     to remove an entry from
   * @return the updated array, without the last occurrence of x
   */
  public static int[] removeLastOccurrence(int x, int[] arr) {
    int skip = arr.length, size = arr.length;
    for(int i = arr.length-1; i >= 0; i--) {
      if(arr[i] == x) {
        size--;
        skip = i;
        break;
      }
      
    }
    int[] result = new int[size];
    for(int i = 0, j = 0; i < size; i++, j++) {
      if(j == skip) {
        j++;
      }
      result[i] = arr[j];
    }
    return result;
  }
}
```
