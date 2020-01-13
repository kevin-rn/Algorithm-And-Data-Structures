In this exercise, you need to implement the method search(int[] a, int x), which checks whether the given array a contains the given integer x as an element in O(logn)

time. The method search should return true if array a contains x as an element, or false otherwise. If the array a is null, then method search should return false as well.

You can assume that the input array a is guaranteed to be sorted in descending order.

Example:
Consider the following array declaration int[] arr = {10, 8, 6, 4, 2, 0};.
The call search(arr, 6) should return true, while the call search(arr, 42) should return false.

IMPORTANT: Your solution must have a worst-case time complexity of O(logn), where n is the size of the input array a.

### Template: 
```java
class Solution {

  /**
   * Checks if the element `x` is in the sorted array `a`, given that `a` is sorted in descending order.
   * This method should have a worst-case time complexity of O(log n).
   * If the input array is null, return false.
   * @param a - the array that needs to be searched
   * @param x - the element we are trying to find
   * @return true if `a` contains `x`, false otherwise
   */
  public static boolean search(int[] a, int x) {
  // TODO
  }
}

```

### Test:
```java
import static org.junit.Assert.*;
import java.lang.annotation.*;
import java.lang.reflect.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;
import org.junit.runner.*;
import org.junit.runner.notification.*;

class TestSuite {

  @SpecTest
  public void testNull() {
    int[] arr = null;
    assertFalse("Null array should return false when searching for element 1", Solution.search(arr, 1));
    assertFalse("Null array should return false when searching for element 2", Solution.search(arr, 2));
  }

  @SpecTest(2)
  public void testExample() {
    int[] arr = { 10, 8, 6, 4, 2, 0 };
    assertTrue("Searching for 6 should return true", Solution.search(arr, 6));
    assertTrue("Searching for 0 should return true", Solution.search(arr, 0));
    assertFalse("Searching for 42 should return false", Solution.search(arr, 42));
    assertFalse("Searching for 5 should return false", Solution.search(arr, 5));
  }

  @SpecTest(2)
  public void testNegativeNumbers() {
    int[] arr = { 100, 50, 31, 3, -42, -99, -123 };
    assertTrue("Searching for 31 should return true", Solution.search(arr, 31));
    assertTrue("Searching for -42 should return true", Solution.search(arr, -42));
    assertFalse("Searching for -1234 should return false", Solution.search(arr, -1234));
    assertFalse("Searching for -12 should return false", Solution.search(arr, -12));
    assertFalse("Searching for 1231 should return false", Solution.search(arr, 1231));
  }

  @SpecTest(5)
  public void testLarge() {
    int[] arr = IntStream.range(0, 360).filter(x -> x % 2 == 0).boxed().sorted(Collections.reverseOrder()).mapToInt(Integer::intValue).toArray();
    for (Integer i : arr) {
      assertTrue("Searching for" + i + "should return true", Solution.search(arr, i));
      assertFalse("Searching for" + (i + 1) + "should return true", Solution.search(arr, i + 1));
    }
  }

  @SpecTest
  public void testTooBig() {
    int[] arr = { 5, 4, 3, 2, 1 };
    assertFalse("Searching for 6 should return false", Solution.search(arr, 6));
    assertFalse("Searching for 7 should return false", Solution.search(arr, 7));
    assertTrue("Searching for 3 should return true", Solution.search(arr, 3));
    assertTrue("Searching for 5 should return true", Solution.search(arr, 5));
  }

  @SpecTest
  public void testTooSmall() {
    int[] arr = { 6, 5, 4, 3, 2 };
    assertFalse("Searching for 0 should return false", Solution.search(arr, 0));
    assertFalse("Searching for 1 should return false", Solution.search(arr, 1));
    assertTrue("Searching for 4 should return true", Solution.search(arr, 4));
    assertTrue("Searching for 2 should return true", Solution.search(arr, 2));
  }
}

/*
 * CODE FROM THIS POINT FORWARD SHOULD NOT BE CHANGED
 */
@RunWith(UTest.class)
public class UTest extends SpecTestRunner {

  /**
   * This constructor gets to know which test suite is under test.
   * But, because WebLab does not allow multiple public classes,
   * the "real" test suite is hardcoded to be `TestSuite` by the Generator.
   * This Runner class must be public because JUnit needs to access its members.
   */
  public UTest(Class<?> testClass) {
    super(TestSuite.class);
  }

  /**
   * This method is automatically called when the tests should be run. These are the steps taken:
   * 1. Instantiate the class to be tested (on WebLab, this will always be TestSuite.class)
   * 2. Search for all methods in the test class that have the @SpecTest annotation
   * 3. Run all tests
   * 4. Use runDummyTests to run 100 dummy tests that pass/fail according to the status of the real tests
   */
  @Override
  public void run(RunNotifier notifier) {
    try {
      testSuite = testClass.newInstance();
      TestMethod[] specTests = getSpecTestMethods();
      Arrays.stream(specTests).forEach(TestMethod::runTest);
      runDummyTests(notifier, specTests);
      System.out.println(out);
    } catch (Exception e) {
      e.printStackTrace();
    }
  }

  /**
   * For each spec-test, check whether it passed or failed and compute the weight.
   * After that, notify the notifier about 100 dummy tests that pass or fail according to the weight that has passed.
   */
  private void runDummyTests(RunNotifier notifier, TestMethod[] specTests) {
    double totalWeight = 0, failWeight = 0;
    for (TestMethod method : specTests) {
      // If the test is a requirement, points are deducted in second loop
      if (method.isRequirement)
        continue;
      if (method.status != Status.PASSED) {
        failWeight += method.weight;
      }
      totalWeight += method.weight;
    }
    failWeight = 100. * failWeight / totalWeight;
    for (TestMethod method : specTests) {
      if (method.isRequirement && method.status != Status.PASSED)
        failWeight += method.weight;
    }
    for (int i = 0; i < 100; i++) {
      Description d = Description.createTestDescription("TestSuite", "Point-" + i);
      notifier.fireTestStarted(d);
      if (i < failWeight)
        notifier.fireTestFailure(new Failure(d, new IgnoreThisFailure()));
      notifier.fireTestFinished(d);
    }
  }

  @Override
  protected String getMethodDescription(TestMethod testMethod) {
    return testMethod.method.getName() + " (" + (testMethod.isRequirement ? "requirement, " : "") + "weight " + testMethod.weight + ")";
  }

  private class IgnoreThisFailure extends Throwable {

    private static final long serialVersionUID = 1L;
  }
}

class SpecTestRunner extends Runner {

  protected Class<?> testClass;

  protected Object testSuite;

  protected boolean abortMission;

  /**
   * We use a StringBuilder instead of System.out to append output from failing tests to.
   * This is because WebLab does not print from a thread.
   * After running all tests, `out` is printed in the main thread.
   */
  protected StringBuilder out = new StringBuilder();

  /**
   * This constructor gets to know which test suite is under test.
   */
  public SpecTestRunner(Class<?> testClass) {
    super();
    this.testClass = testClass;
  }

  @Override
  public Description getDescription() {
    return Description.createSuiteDescription(testClass);
  }

  /**
   * This method is automatically called when the tests should be run. These are the steps taken:
   * 1. Instantiate the class to be tested
   * 2. Search for all methods in the test class that have the @SpecTest annotation
   * 3. Run all tests and notify the notifier about the results
   */
  @Override
  public void run(RunNotifier notifier) {
    try {
      testSuite = testClass.newInstance();
      Arrays.stream(getSpecTestMethods()).forEach(testMethod -> {
        notifier.fireTestStarted(testMethod.description);
        testMethod.runTest();
        if (testMethod.status != Status.PASSED)
          notifier.fireTestFailure(new Failure(testMethod.description, testMethod.exception));
        notifier.fireTestFinished(testMethod.description);
      });
      System.out.println(out);
    } catch (Exception e) {
      e.printStackTrace();
    }
  }

  protected TestMethod[] getSpecTestMethods() {
    return Arrays.stream(testClass.getMethods()).filter(m -> m.getAnnotation(SpecTest.class) != null && (m.getModifiers() & Modifier.STATIC) == 0).map(TestMethod::new).sorted(Comparator.comparingInt(method -> method.order)).toArray(TestMethod[]::new);
  }

  protected enum Status {

    NOT_STARTED, PASSED, FAILED, TIMED_OUT
  }

  protected String getMethodDescription(TestMethod testMethod) {
    return testMethod.method.getName();
  }

  protected class TestMethod {

    Method method;

    Description description;

    Status status;

    Throwable exception;

    int weight;

    int order;

    long timeout;

    boolean isRequirement;

    protected TestMethod(Method method) {
      this.method = method;
      status = Status.NOT_STARTED;
      SpecTest annotation = method.getAnnotation(SpecTest.class);
      weight = annotation.value();
      order = annotation.order();
      timeout = annotation.timeout();
      isRequirement = method.getAnnotation(Requirement.class) != null;
      description = Description.createTestDescription(testClass, getMethodDescription(this));
    }

    protected void runTest() {
      if (abortMission) {
        failTest(description, new TestTimedOutException(timeout, TimeUnit.MILLISECONDS));
      } else {
        status = timeout > 0 ? runTestWithTimeout() : runTestWithoutTimeout();
      // Abort mission when one test times out was an attempt to reduce load on the WebLab servers,
      // but the annoyance of flaky test scores is more important right now as there seems to be enough hardware.
      // if (status == Status.TIMED_OUT) {
      // out.append("Test ").append(method.getName()).append(" timed out, not executing the rest of the tests.\n");
      // abortMission = true;
      // }
      }
    }

    private Status runTestWithoutTimeout() {
      try {
        method.invoke(testSuite);
        return Status.PASSED;
      } catch (InvocationTargetException e) {
        failTest(description, e.getTargetException());
        return Status.FAILED;
      } catch (Throwable e) {
        failTest(description, e);
        return Status.FAILED;
      }
    }

    private Status runTestWithTimeout() {
      try {
        return Executors.newSingleThreadExecutor().submit(this::runTestWithoutTimeout).get(timeout, // throws the exception if one occurred during the invocation
        TimeUnit.MILLISECONDS);
      } catch (TimeoutException e) {
        failTest(description, new TestTimedOutException(timeout, TimeUnit.MILLISECONDS));
        return Status.TIMED_OUT;
      } catch (ExecutionException e) {
        failTest(description, e.getCause());
        return Status.FAILED;
      } catch (Throwable e) {
        failTest(description, e);
        return Status.FAILED;
      }
    }

    private void failTest(Description d, Throwable e) {
      exception = e;
      out.append(d.getMethodName()).append(" failed: ").append(e).append('\n');
      for (StackTraceElement s : e.getStackTrace()) {
        if (s.getMethodName().startsWith("invoke"))
          break;
        out.append("    ").append(s).append('\n');
        if (s.getMethodName().equals("runTest"))
          break;
      }
    }
  }

  /**
   * Clone of the JUnit 4.12 class. Apparently not available on WebLab.
   */
  protected class TestTimedOutException extends Exception {

    private static final long serialVersionUID = 31935685163547539L;

    /**
     * Creates exception with a standard message "test timed out after [timeout] [timeUnit]"
     *
     * @param timeout  the amount of time passed before the test was interrupted
     * @param timeUnit the time unit for the timeout value
     */
    TestTimedOutException(long timeout, TimeUnit timeUnit) {
      super(String.format("test timed out after %d %s", timeout, timeUnit.name().toLowerCase()));
    }
  }
}

@Retention(RetentionPolicy.RUNTIME)
@Target({ ElementType.METHOD })
@interface SpecTest {

  class None extends Throwable {

    private static final long serialVersionUID = 1L;

    private None() {
    }
  }

  /**
   * @return The weight of this SpecTest.
   */
  int value() default 1;

  int order() default -1;

  // FIXME not taken into account yet
  Class<? extends Throwable> expected() default None.class;

  long timeout() default 0L;
}

@Retention(RetentionPolicy.RUNTIME)
@Target({ ElementType.METHOD })
@interface Requirement {
}

```

__________________________________________________________________________________________________________________

### Iterative Solution:
```java
class Solution {

  /**
   * Checks if the element `x` is in the sorted array `a`, given that `a` is sorted in descending order.
   * This method should have a worst-case time complexity of O(log n).
   * If the input array is null, return false.
   * @param a - the array that needs to be searched
   * @param x - the element we are trying to find
   * @return true if `a` contains `x`, false otherwise
   */
  public static boolean search(int[] a, int x) {
    if (a == null) {
      return false;
    }
    int low = 0;
    int high = a.length - 1;
    while (high >= low) {
      int mid = (high + low) / 2;
      if (a[mid] == x) {
        return true;
      } else if (a[mid] > x) {
        low = mid + 1;
      } else {
        high = mid - 1;
      }
    }
    return false;
  }
}

```

### Recursive Solution:
```
class Solution {

  /**
   * Checks if the element `x` is in the sorted array `a`, given that `a` is sorted in descending order.
   * This method should have a worst-case time complexity of O(log n).
   * If the input array is null, return false.
   * @param a - the array that needs to be searched
   * @param x - the element we are trying to find
   * @return true if `a` contains `x`, false otherwise
   */
  public static boolean search(int[] a, int x) {
    if(a == null) return false;
    return check(a, x, 0, a.length-1);
  }
  
  public static boolean check(int[] a, int x, int low, int high) {
    if(low > high) return false;
    int mid = (low+high)/2;
    if(a[mid] == x) return true;
    else if(a[mid] < x) return check(a, x, low, mid-1);
    else return check(a, x, mid+1, high);
  }
  
}


```

