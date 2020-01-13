In this exercise, you need to implement the method upperCount(int[] a, int k), which checks whether each integer element in the given array a appears at most k times. The method upperCount should return true if and only if each integer appears at most k times in the array a, and false otherwise. If the array a is null, the method should return true.

You can assume that k >= 0 and that a.length > 0.

Example:
Given the array declaration int[] a = {2, 3, 1, 4, 5, 1, 7, 0};, the call upperCount(a,2) should return true, while the call upperCount(a,1) should return false.

IMPORTANT: Your solution needs to make use of the heap-based priority queue that is provided in the library. You are not allowed to use any additional auxiliary algorithms and data structures beyond those included in the library and the template solution.

IMPORTANT: Your solution should have a worst-case time complexity of O(nlogn)
, where n

is the size of the array a.

IMPORTANT: Your solution will be manually checked to see if you have actually implemented the exercise and have not cheated the spec-test system in any way. Depending on that, points may be deducted.

You are given an implementation of a heap-based priority queue in the library code, containing the following methods that you can use:

```java
class LibraryPQ { 
  // Creates an empty priority queue (PQ).
  public LibraryPQ();

  // Inserts element 'i' into this PQ.
  public void insert(int i);

  // Removes the maximal element from this PQ.
  public int removeMax();

  // Returns the number of elements in this PQ.
  public int size();
  
  // Returns true if this PQ is empty, false otherwise.
  public boolean isEmpty();
}
```

### Template:
```java
class Solution {

  /**
   * Checks if every integer element in the array `a` appears at most `k` times.
   * This method should have a worst-case time complexity of O(n log n).
   * If the input array is null, return true.
   * @param a - the array to search
   * @param k - the maximum number of times each unique element should appear in the array
   * @return true if each integer element appears at most 'k' times in 'a', false otherwise
   */
  public static boolean upperCount(int[] a, int k) {
  // TODO
  }
}

```

### Library:
```java
import java.util.*;

class LibraryPQ {

  private List<Integer> heap;

  public LibraryPQ() {
    heap = new ArrayList<>();
  }

  /**
   * Swaps two elements in the list.
   *
   * @param i
   *     Position of element to swap in a.
   * @param j
   *     Position of element to swap in a.
   */
  private void swap(int i, int j) {
    int t = heap.get(i);
    heap.set(i, heap.get(j));
    heap.set(j, t);
  }

  /**
   * Restores the heap property in a heap represented as an arraylist.
   * When the heap property is invalid at root,
   * the method fixes the heap first locally before fixing the affected subtree.
   *
   * @param root
   *     Index of the root of the heap, which might be a subtree of the overall heap.
   * @param range
   *     Index of the last element in the heap, array elements with an index > range are not part of the heap.
   */
  private void downHeap(int root, int range) {
    // index of left and right children
    int left = 2 * root + 1;
    int right = 2 * root + 2;
    int largest;
    if (left <= range && heap.get(left) > heap.get(root))
      largest = left;
    else
      largest = root;
    if (right <= range && heap.get(right) > heap.get(largest))
      largest = right;
    // heap property invalid at root
    if (largest != root) {
      swap(root, largest);
      downHeap(largest, range);
    }
  }

  /**
   * Restores the heap property in a heap represented as an arraylist.
   * The method compares the node to its parent and swaps if necessary.
   *
   * @param i index of the node
   */
  private void upHeap(int i) {
    while (i >= 1) {
      int j = (i - 1) / 2;
      if (heap.get(j) >= heap.get(i))
        break;
      swap(j, i);
      i = j;
    }
  }

  /**
   * Inserts the specified element into this priority queue.
   *
   * @param i
   *     element to add
   */
  public void insert(int i) {
    heap.add(i);
    upHeap(heap.size() - 1);
  }

  /**
   * Retrieves and removes the first element of this priority queue.
   *
   * @return the first element of the queue
   */
  public int removeMax() {
    int i = heap.get(0);
    swap(0, heap.size() - 1);
    heap.remove(heap.size() - 1);
    downHeap(0, heap.size() - 1);
    return i;
  }

  /**
   * @return the current number of elements in the heap
   */
  public int size() {
    return this.heap.size();
  }

  /**
   * @return true if the heap is empty, else false
   */
  public boolean isEmpty() {
    return this.heap.size() == 0;
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
import org.junit.runner.*;
import org.junit.runner.notification.*;

class TestSuite {

  @SpecTest
  public void testNull() {
    int[] a = null;
    assertTrue("Null array should return true with number 1", Solution.upperCount(a, 1));
    assertTrue("Null array should return true with number 2", Solution.upperCount(a, 2));
  }

  @SpecTest(2)
  public void testExample() {
    int[] a = { 2, 3, 1, 4, 5, 1, 7, 0 };
    assertTrue("Method should return true with count at most 2", Solution.upperCount(a, 2));
    assertFalse("Method should return false with count at most 1", Solution.upperCount(a, 1));
  }

  @SpecTest(2)
  public void testSorted() {
    int[] a = { 3, 4, 12, 42, 42, 42, 51, 123, 443, 4223 };
    assertTrue("Method should return true with count at most 3", Solution.upperCount(a, 3));
    assertFalse("Method should return false with count at most 2", Solution.upperCount(a, 2));
    assertTrue("Method should return true with count at most 4", Solution.upperCount(a, 4));
  }

  @SpecTest(2)
  public void testNegative() {
    int[] a = { -1, -24, 12, -123, 1, 1, -2, -2, 12, -2 };
    assertFalse("Method should return false with count at most 2", Solution.upperCount(a, 2));
    assertTrue("Method should return true with count at most 3", Solution.upperCount(a, 3));
    assertFalse("Method should return false with count at most 1", Solution.upperCount(a, 1));
  }

  @SpecTest(3)
  public void testLarge() {
    int[] a = new Random(123).ints(0, 10).limit(100).toArray();
    assertTrue("Method should return true with count at most 15", Solution.upperCount(a, 15));
    assertTrue("Method should return true with count at most 13", Solution.upperCount(a, 13));
    assertFalse("Method should return false with count at most 12", Solution.upperCount(a, 12));
    assertFalse("Method should return false with count at most 9", Solution.upperCount(a, 9));
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

___________________________________________________________________________________________________________________

### My Solution:
```java
class Solution {

  /**
   * Checks if every integer element in the array `a` appears at most `k` times.
   * This method should have a worst-case time complexity of O(n log n).
   * If the input array is null, return true.
   * @param a - the array to search
   * @param k - the maximum number of times each unique element should appear in the array
   * @return true if each integer element appears at most 'k' times in 'a', false otherwise
   */
  public static boolean upperCount(int[] a, int k) {
    if(a == null) return true;
    LibraryPQ pq = new LibraryPQ();
    for(int sort : a) pq.insert(sort);
    for(int i = 0; i < a.length; i++) a[a.length-i-1] = pq.removeMax();
    
    int current = a[0], total = 1;
    for(int i = 1; i < a.length; i++) {
      if(a[i] > current) {
        current = a[i];
        total = 1;
      } else {
        total++;
        if(total > k) return false;
      }
    }
    return true;
  }
}
```

### Official Solution:
```java
class Solution {

  /**
   * Checks if every integer element in the array `a` appears at most `k` times.
   * This method should have a worst-case time complexity of O(n log n).
   * If the input array is null, return true.
   * @param a - the array to search
   * @param k - the maximum number of times each unique element should appear in the array
   * @return true if each integer element appears at most 'k' times in 'a', false otherwise
   */
  public static boolean upperCount(int[] a, int k) {
    if (a == null) {
      return true;
    }
    LibraryPQ pq = new LibraryPQ();
    for (Integer i : a) {
      pq.insert(i);
    }
    int count = 1;
    int value = Integer.MIN_VALUE;
    while (!pq.isEmpty()) {
      int current = pq.removeMax();
      if (value != current) {
        value = current;
        count = 1;
      } else {
        count++;
        if (count > k) {
          return false;
        }
      }
    }
    return true;
  }
}
```
