In this exercise we will implement the method to compute the nth number in the Fibonacci sequence recursively again.   
However, this time we will have a limitation: you are only allowed to make one recursive call.  

For this purpose a helper method might be useful and the signature of this helper method has been provided.   
The idea is to use two extra arguments to keep track of intermediate results that could be reused.  

```java
class Solution {

  /**
   * Computes the nth number in the Fibonacci sequence.
   * @param n - the index of the number in the Fibonacci sequence.
   * @return nth number in the Fibonacci sequence
   */
  public static int fibonacci(int n) {
    return fibonacci_helper(n, 0, 1);
  }

  /**
   * Helper function for computing the nth number in the Fibonacci sequence.
   * @param n - the index of the number in the Fibonacci sequence.
   * @param acc1 - accumulator for the previous number in the Fibonacci sequence.
   * @param acc2 -accumulator for the previous number in the Fibonacci sequence.
   * @return
   */
  public static int fibonacci_helper(int n, int acc1, int acc2) {
  if (n == 0) return acc1; 
  if (n == 1) return acc2; 
  return fibonacci_helper(n - 1, acc2, acc1 + acc2); 
  }
}
```
