In this exercise, you need to implement the method sum(Tree t1, Tree t2). This method creates and returns a new tree based on the two n-ary input trees t1and t2. The value of each node in the resulting tree should be obtained by adding the values of the nodes at the same positions in the two input n-ary trees t1 and t2.

Note that trees t1 and t2 are guaranteed to have the same shape, and the resulting tree should also have this shape.

For example, summing the two trees below

    1          5
  / | \      / | \
 2  3  4    6  7  8

will return the following tree

    6   
  / | \ 
 8 10  12

IMPORTANT: Your implementation must return a new tree. The original trees should not be changed.

IMPORTANT: Your solution will be manually checked to see if you have actually implemented the exercise and have not cheated the spec-test system in any way. Depending on that, points may be deducted.

In the library code you will find an implementation for an n-ary tree, containing the following methods:

```java
class Tree {
  // Creates a tree with a value and no children.
  public Tree(int value);

  // Creates a tree with a value and children.
  public Tree(int value, List<Tree> children);

  // Returns the value of this tree.
  public int getValue();

  // Returns the children of this tree.
  public List<Tree> getChildren();  

  // Returns true when 'other' is identical to this tree.
  public boolean equals(Object other);

  // Returns a readable string representation of this tree.
  public String toString();
}
```


### Template:
```java
import java.util.*;

class Solution {

  /**
   * Sums the values of the nodes of two n-ary trees.
   * @param t1 - first tree to sum values for
   * @param t2 - second tree to sum values for
   * @return a new tree in which every node contains the sum of the values of the nodes at the corresponding positions in t1 and t2
   */
  public static Tree sum(Tree t1, Tree t2) {
  // TODO
  }
}

```

### Library:
```java
import java.util.*;

class Tree {

  private int value;

  private List<Tree> children;

  /**
   * Creates a tree with the given value, and no children.
   * @param value The value for this tree.
   */
  public Tree(int value) {
    this.children = new LinkedList<>();
    this.value = value;
  }

  /**
   * Creates a tree with the given value and list of children.
   * @param value The value for this tree.
   * @param children The subtrees for this tree.
   */
  public Tree(int value, List<Tree> children) {
    this.children = new LinkedList<>(children);
    this.value = value;
  }

  /**
   * Returns the value of this tree.
   * @return The value of this tree.
   */
  public int getValue() {
    return value;
  }

  /**
   * Returns the subtrees of this tree.
   * @return The subtrees of this tree.
   */
  public List<Tree> getChildren() {
    return this.children;
  }

  /**
   * Checks equality of two trees.
   * @param other The object to compare with.
   * @return True if the trees are equal, false otherwise.
   */
  public boolean equals(Object other) {
    if (other instanceof Tree) {
      Tree that = (Tree) other;
      return that.getValue() == this.getValue() && this.getChildren().equals(that.getChildren());
    }
    return false;
  }

  /**
   * Returns a human readable format of this tree.
   * @return A string representation of this tree.
   */
  public String toString() {
    StringBuilder sb = new StringBuilder();
    this.toString(sb, 0);
    return sb.toString();
  }

  /**
   * Returns a human readable format of this tree.
   * @param sb StringBuilder to append to.
   * @param depth Identation depth of this part.
   */
  private void toString(StringBuilder sb, int depth) {
    for (int i = 0; i < depth; i++) sb.append("  ");
    sb.append("<Tree ").append(this.value).append(" [");

    if (this.children.isEmpty()) {
      sb.append("]>");
      return;
    }
    // Recursively add children
    for (Tree t : this.children) {
      sb.append("\n");
      for (int i = 0; i < depth; i++) sb.append("  ");
      t.toString(sb, depth + 1);
    }
    sb.append("\n");
    for (int i = 0; i < depth; i++) sb.append("  ");
    sb.append("]>");
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
  public void testExample() {
    Tree t1 = new Tree(1, Arrays.asList(new Tree(2), new Tree(3), new Tree(4)));
    Tree t2 = new Tree(5, Arrays.asList(new Tree(6), new Tree(7), new Tree(8)));
    Tree res = new Tree(6, Arrays.asList(new Tree(8), new Tree(10), new Tree(12)));
    assertEquals(res, Solution.sum(t1, t2));
  }

  @SpecTest
  public void testOneNode() {
    Tree t1 = new Tree(5);
    Tree t2 = new Tree(19);
    assertEquals(new Tree(24), Solution.sum(t1, t2));
  }

  @SpecTest
  public void testSmall() {
    Tree t1 = new Tree(42, Arrays.asList(new Tree(1), new Tree(2)));
    Tree t2 = new Tree(16, Arrays.asList(new Tree(92), new Tree(53)));
    Tree res = new Tree(58, Arrays.asList(new Tree(93), new Tree(55)));
    assertEquals(res, Solution.sum(t1, t2));
    assertEquals(res, Solution.sum(t2, t1));
  }

  /**
   * Sums
   *
   *       (      104      )
   *       /         |     \
   *   (  491  )   ( 16 )  9
   *   / |  |  \   / |  \
   *  1  2  3  4  5  6  7
   *
   * and
   *
   *       (      22       )
   *       /         |     \
   *    (  13  )   ( 93 )  16
   *   / |  |  \   / |  \
   *  9  8  4  7  1  5  6
   */
  @SpecTest(2)
  public void testThreeLevels() {
    Tree t1 = new Tree(104, Arrays.asList(new Tree(491, Arrays.asList(new Tree(1), new Tree(2), new Tree(3), new Tree(4))), new Tree(16, Arrays.asList(new Tree(5), new Tree(6), new Tree(7))), new Tree(9)));
    Tree t2 = new Tree(22, Arrays.asList(new Tree(13, Arrays.asList(new Tree(9), new Tree(8), new Tree(4), new Tree(7))), new Tree(93, Arrays.asList(new Tree(1), new Tree(5), new Tree(6))), new Tree(16)));
    Tree res = new Tree(126, Arrays.asList(new Tree(504, Arrays.asList(new Tree(10), new Tree(10), new Tree(7), new Tree(11))), new Tree(109, Arrays.asList(new Tree(6), new Tree(11), new Tree(13))), new Tree(25)));
    assertEquals(res, Solution.sum(t1, t2));
    assertEquals(res, Solution.sum(t2, t1));
  }

  /**
   * Sums
   *
   *       (       104       )
   *       /       |   |     \
   *   (  491  )  16   9     92
   *   / |  |  \      / \
   *  1  2  3  4    72  22
   *                    |
   *                    51
   *
   * and
   *
   *       (       309       )
   *       /       |   |     \
   *   (  124  )  53   9     41
   *   / |  |  \      / \
   *  9  17 6  47   68  20
   *                    |
   *                    13
   */
  @SpecTest(2)
  public void testFourLevels() {
    Tree t1 = new Tree(104, Arrays.asList(new Tree(491, Arrays.asList(new Tree(1), new Tree(2), new Tree(3), new Tree(4))), new Tree(16), new Tree(9, Arrays.asList(new Tree(68), new Tree(22, Arrays.asList(new Tree(51))))), new Tree(92)));
    Tree t2 = new Tree(309, Arrays.asList(new Tree(124, Arrays.asList(new Tree(9), new Tree(17), new Tree(6), new Tree(47))), new Tree(53), new Tree(9, Arrays.asList(new Tree(72), new Tree(20, Arrays.asList(new Tree(13))))), new Tree(41)));
    Tree res = new Tree(413, Arrays.asList(new Tree(615, Arrays.asList(new Tree(10), new Tree(19), new Tree(9), new Tree(51))), new Tree(69), new Tree(18, Arrays.asList(new Tree(140), new Tree(42, Arrays.asList(new Tree(64))))), new Tree(133)));
    assertEquals(res, Solution.sum(t1, t2));
    assertEquals(res, Solution.sum(t2, t1));
  }

  @SpecTest(2)
  public void testRandom1() {
    Tree[] trees = generateTrees(new Random(40184), 6, 7);
    assertEquals(trees[2], downCast(Solution.sum(trees[0], trees[1])));
  }

  @SpecTest(2)
  public void testRandom2() {
    Tree[] trees = generateTrees(new Random(39192), 10, 9);
    assertEquals(trees[2], downCast(Solution.sum(trees[0], trees[1])));
  }

  @SpecTest(2)
  public void testRandom3() {
    Tree[] trees = generateTrees(new Random(82730), 11, 13);
    assertEquals(trees[2], downCast(Solution.sum(trees[0], trees[1])));
  }

  @Requirement
  @SpecTest(100)
  public void testNewTree() {
    Tree t1 = new Tree(42, Arrays.asList(new Tree(1), new Tree(2)));
    Tree t2 = new Tree(42, Arrays.asList(new Tree(1), new Tree(2)));
    Tree t3 = new Tree(16, Arrays.asList(new Tree(92), new Tree(53)));
    Tree t4 = new Tree(16, Arrays.asList(new Tree(92), new Tree(53)));
    Tree res = Solution.sum(t1, t3);
    assertEquals("Original trees should be unchanged", t2, t1);
    assertEquals("Original trees should be unchanged", t4, t3);
    assertFalse(res == t1 || res == t3);
  }

  /**
   * Transforms a regular Tree into a SpecTestTree.
   * @param tree Tree to transform.
   * @return SpecTestTree version of the given Tree.
   */
  public SpecTestTree downCast(Tree tree) {
    return new SpecTestTree(tree.getValue(), tree.getChildren().stream().map(this::downCast).collect(Collectors.toList()));
  }

  /**
   * Compares 2 Trees after overriding their toString.
   * @param t1 First tree to compare.
   * @param t2 Second tree to compare.
   */
  public void assertEquals(Tree t1, Tree t2) {
    org.junit.Assert.assertEquals(downCast(t1), downCast(t2));
  }

  /**
   * Compares 2 Trees after overriding their toString.
   * @param msg Assertion message.
   * @param t1 First tree to compare.
   * @param t2 Second tree to compare.
   */
  public void assertEquals(String msg, Tree t1, Tree t2) {
    org.junit.Assert.assertEquals(msg, downCast(t1), downCast(t2));
  }

  /**
   * Creates 3 random trees within the given bounds.
   * @param rnd Random to use for values.
   * @param maxDepth Maximum depth of this tree.
   * @param maxWidth Maximum width of this tree.
   * @return An array containing three Trees. The last one sums the other 2.
   */
  public Tree[] generateTrees(Random rnd, int maxDepth, int maxWidth) {
    int v1 = rnd.nextInt(1000);
    int v2 = rnd.nextInt(1000);
    if (maxDepth == 0) {
      return new Tree[] { new Tree(v1), new Tree(v2), new Tree(v1 + v2) };
    }
    List<Tree> children1 = new LinkedList<>();
    List<Tree> children2 = new LinkedList<>();
    List<Tree> children3 = new LinkedList<>();
    int width = rnd.nextInt(maxWidth) + 1;
    for (int i = 0; i < width; i++) {
      int depth = maxDepth == 1 ? 0 : rnd.nextInt(maxDepth);
      Tree[] c = generateTrees(rnd, depth, maxWidth);
      children1.add(c[0]);
      children2.add(c[1]);
      children3.add(c[2]);
    }
    return new Tree[] { new Tree(v1, children1), new Tree(v2, children2), new Tree(v1 + v2, children3) };
  }
}

class SpecTestTree extends Tree {

  public SpecTestTree(int value) {
    super(value);
  }

  public SpecTestTree(int value, List<Tree> children) {
    super(value, children);
  }

  /**
   * Removes all the noise from the spec-test output.
   * @return A much more compact string representation of this tree.
   */
  @Override
  public String toString() {
    return "<Tree " + this.getValue() + " , " + this.getChildren().size() + " children >";
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

______________________________________________________________________________________________________________

### My Solution (more code):
```java
import java.util.*;

class Solution {

  /**
   * Sums the values of the nodes of two n-ary trees.
   * @param t1 - first tree to sum values for
   * @param t2 - second tree to sum values for
   * @return a new tree in which every node contains the sum of the values of the nodes at the corresponding positions in t1 and t2
   */
  public static Tree sum(Tree t1, Tree t2) {
    if(t1.getChildren().isEmpty() && t2.getChildren().isEmpty()) return new Tree(t1.getValue()+t2.getValue());
    if(t1.getChildren().isEmpty()) return new Tree(t1.getValue()+t2.getValue(), t2.getChildren());
    if(t2.getChildren().isEmpty()) return new Tree(t1.getValue()+t2.getValue(), t1.getChildren());
    ArrayList<Tree> childs = new ArrayList<>();
    List<Tree> a = t1.getChildren(), b = t2.getChildren();
      for(int i = 0; i<a.size(); i++ ) {
        childs.add(sum(a.get(i),b.get(i)));
      }
    Tree root = new Tree(t1.getValue()+t2.getValue(), childs);
    return root;
  }
}


```

### Official Solution:
````java
class Solution {

  /**
   * Sums the values of the nodes of two n-ary trees.
   * @param t1 - first tree to sum values for
   * @param t2 - second tree to sum values for
   * @return a new tree in which every node contains the sum of the values of the nodes at the corresponding positions in t1 and t2
   */
  public static Tree sum(Tree t1, Tree t2) {
    Tree res = new Tree(t1.getValue() + t2.getValue());
    for (int i = 0; i < t1.getChildren().size(); i++) {
      res.getChildren().add(sum(t1.getChildren().get(i), t2.getChildren().get(i)));
    }
    return res;
  }
}

```
