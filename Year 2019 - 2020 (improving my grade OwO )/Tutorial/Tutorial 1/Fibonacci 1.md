In this exercise you will have to implement a method that given an integer n, computes the nth number in the Fibonacci sequence in a recursive manner.

Fibonacci sequence is the sequence of numbers:

1, 1, 2, 3, 5, 8, 13, 21, 34, ...

Notice that there is a pattern in this sequence. The first number in this sequence is 1, the second number is 1 as well, the third number is 2, which is equal to the first number plus the second number. The fourth number is 3, which is equal to the second number plus the fourth number. Each number after the first two will be sum of the previous number and the one before that. So for every n >= 3, fib(n) = fib(n-1) + fib(n-2). You can verify that this is indeed the case.

Your method will need to return the nth number in this sequence. Note that the 0th number in the sequence is 0.

Note: you are not allowed to use helper methods (i.e. your implementation should not include another method other than the one we have provided).

```java
class Solution {

  /**
   * Computes the nth number in the Fibonacci sequence.
   * @param n - the index of the number in the Fibonacci sequence.
   * @return nth number in the Fibonacci sequence
   */
  public static int fibonacci(int n) {
    if(n == 0) return 0;
    if(n == 1 || n == 2) return 1;
    return fibonacci(n-1) + fibonacci(n-2);
  }
}
```
