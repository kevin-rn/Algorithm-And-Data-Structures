In this exercise, you need to implement a queue using a fixed-size circular array. You are given a template for the ArrayQueue class. You need to implement the constructor method, as well as the enqueue and dequeue methods. The enqueue and dequeue methods should have a time complexity of O(1)

.

The enqueue method should throw a FullQueueException when the queue is full. The dequeue method should throw an EmptyQueueException when the queue is empty. You can find the implementations for these exceptions in the library code.

You can assume the capacity of the ArrayQueue will always be positive.

IMPORTANT: You are not allowed to use any auxiliary data structures beyond the array field that is already provided in the class template. You are allowed to create additional methods and primitive fields if necessary (e.g. float, int, String, …).

IMPORTANT: The enqueue and dequeue methods need to work in O(1) time.

### Template:
```java
class ArrayQueue {

  private int[] arr;

  /**
   * Creates a new ArrayQueue with the given capacity.
   * @param capacity the capacity for this queue
   */
  public ArrayQueue(int capacity) {
  // TODO
  }

  /**
   * Adds the given element to the queue.
   * @param e the element to add to the queue
   * @throws FullQueueException if the queue is full
   */
  public void enqueue(int e) throws FullQueueException {
  // TODO
  }

  /**
   * Removes an element from the queue and returns it.
   * @return the first element in the queue
   * @throws EmptyQueueException if the queue is empty
   */
  public int dequeue() throws EmptyQueueException {
  // TODO
  }
}

```

### Library:
```java
class EmptyQueueException extends RuntimeException {

  private static final long serialVersionUID = 42L;
}

class FullQueueException extends RuntimeException {

  private static final long serialVersionUID = 42L;
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
  public void testExample() {
    ArrayQueue q = new ArrayQueue(20);
    for (int i = 0; i < 10; i++) {
      q.enqueue(i);
    }
    for (int i = 0; i < 10; i++) {
      assertEquals(i, q.dequeue());
    }
  }

  @SpecTest
  public void testLarge() {
    ArrayQueue q = new ArrayQueue(12000);
    List<Integer> nums = new ArrayList<>();
    Random rnd = new Random(184612);
    for (int x = 0; x < 11698; x++) {
      int num = rnd.nextInt(420);
      nums.add(num);
      q.enqueue(num);
    }
    for (int num : nums) {
      assertEquals(num, q.dequeue());
    }
  }

  @Requirement
  @SpecTest(100)
  public void testCircularArray() {
    ArrayQueue q = new ArrayQueue(25);
    for (int x = 0; x < 116; x++) {
      q.enqueue(x);
      q.dequeue();
    }
  // No assertions in this test. It purely tests the queue doesn't crash
  // after the full array should be traversed.
  }

  @SpecTest(4)
  public void testEnqueueDequeueMany() {
    ArrayQueue q = new ArrayQueue(74);
    int[] nums = new int[220];
    Random rnd = new Random(401941);
    for (int x = 0; x < 220; x++) {
      int num = rnd.nextInt(360);
      nums[x] = num;
      // System.out.print(num);
      // System.out.print(" ");
    }
    // System.out.println();
    int i = 0;
    int j = 0;
    while (i < 50) {
      q.enqueue(nums[i++]);
    }
    while (j < 18) {
      assertEquals(nums[j++], q.dequeue());
    }
    while (i < 92) {
      q.enqueue(nums[i++]);
    }
    while (j < 79) {
      assertEquals(nums[j++], q.dequeue());
    }
    while (i < 120) {
      q.enqueue(nums[i++]);
    }
    while (j < 120) {
      assertEquals(nums[j++], q.dequeue());
    }
    while (i < 159) {
      q.enqueue(nums[i++]);
    }
    while (j < 141) {
      assertEquals(nums[j++], q.dequeue());
    }
    while (i < 210) {
      q.enqueue(nums[i++]);
    }
    while (j < 190) {
      assertEquals(nums[j++], q.dequeue());
    }
    while (i < 220) {
      q.enqueue(nums[i++]);
    }
    while (j < 220) {
      assertEquals(nums[j++], q.dequeue());
    }
  }

  @SpecTest
  public void testMaxCap() {
    ArrayQueue q = new ArrayQueue(9);
    for (int i = 0; i < 9; i++) {
      q.enqueue(i);
    }
    for (int i = 0; i < 9; i++) {
      assertEquals(i, q.dequeue());
    }
  }

  @SpecTest
  public void testTooMany() {
    ArrayQueue q = new ArrayQueue(9);
    for (int i = 0; i < 9; i++) {
      q.enqueue(i);
    }
    boolean caught = false;
    try {
      q.enqueue(6);
    } catch (FullQueueException e) {
      caught = true;
    }
    assertTrue(caught);
  }

  @SpecTest
  public void testDequeueEmpty() {
    ArrayQueue q = new ArrayQueue(9);
    for (int i = 0; i < 9; i++) {
      q.enqueue(i);
    }
    for (int i = 0; i < 9; i++) {
      q.dequeue();
    }
    boolean caught = false;
    try {
      q.dequeue();
    } catch (EmptyQueueException e) {
      caught = true;
    }
    assertTrue(caught);
  }

  @SpecTest(timeout = 500)
  public void testComplexity() {
    ArrayQueue q = new ArrayQueue(600_000);
    for (int i = 0; i < 500_000; i++) {
      q.enqueue(i);
    }
    for (int i = 0; i < 500_000; i++) {
      q.dequeue();
    }
  // No assertions in this test. It purely tests the time the operations take.
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

_________________________________________________________________________________________________

### Solution: 
```java
class ArrayQueue {

  private int[] arr;

  private int head;

  private int size;

  /**
   * Creates a new ArrayQueue with the given capacity.
   * @param capacity the capacity for this queue
   */
  public ArrayQueue(int capacity) {
    this.arr = new int[capacity];
    this.head = 0;
    this.size = 0;
  }

  /**
   * Adds the given element to the queue.
   * @param e the element to add to the queue
   * @throws FullQueueException if the queue is full
   */
  public void enqueue(int e) throws FullQueueException {
    if (size == arr.length) {
      throw new FullQueueException();
    }
    arr[(head + size++) % arr.length] = e;
  }

  /**
   * Removes an element from the queue and returns it.
   * @return the first element in the queue
   * @throws EmptyQueueException if the queue is empty
   */
  public int dequeue() throws EmptyQueueException {
    if (size == 0) {
      throw new EmptyQueueException();
    }
    int res = arr[head];
    head = (head + 1) % arr.length;
    size--;
    return res;
  }
}

```
