In this assignment you have to implement the method countNodesEvenChildren, which counts the number of nodes in a tree that have an even number of children.

The method takes as input a tree data structure of type LibraryTree, and should return the number of nodes in the given tree that have an even number of children.

Only nodes that are non-null are counted as children.

The method should return 0, if the tree is null.

In the library, you can find an implementation of the class LibraryTree.

### Template:
```java
class Solution {
  /**
   * Counts the number of nodes with an event number of children.
   *
   * @param tree
   *     The tree to count nodes with an even number of children in.
   * @return the number of nodes with an even number of children, or 0 if tree is null.
   */
  public static int countNodesEvenChildren(LibraryTree tree) {
    // TODO
  }
}

```

### Library:
```java
import java.util.*;

class LibraryTree {
  private int key;
  private List<LibraryTree> children;

  public LibraryTree(int key) {
    this.key = key;
    children = new ArrayList<>();
  }

  public LibraryTree(int key, List<LibraryTree> children) {
    this.key = key;
    this.children = children;
  }

  public int getKey() {
    return this.key;
  }

  public List<LibraryTree> getChildren() {
    return this.children;
  }
}

```

### Test:
```java
import static org.junit.Assert.*;

import java.util.*;

import org.junit.*;

public class UTest {
  @Test
  public void testNull() {
    LibraryTree tree = null;
    assertEquals(0, Solution.countNodesEvenChildren(tree));
  }

  @Test
  public void testRoot() {
    LibraryTree tree = new LibraryTree(0);
    assertEquals(1, Solution.countNodesEvenChildren(tree));
  }

  @Test
  public void testSmall() {
    LibraryTree tree = new LibraryTree(0, Arrays.asList(new LibraryTree(1), new LibraryTree(2)));
    assertEquals(3, Solution.countNodesEvenChildren(tree));
  }
}


```

____________________________________________________________________________________________________

### Solution:
```java
class Solution {
  /**
   * Counts the number of nodes with an event number of children.
   *
   * @param tree
   *     The tree to count nodes with an even number of children in.
   * @return the number of nodes with an even number of children, or 0 if tree is null.
   */
  public static int countNodesEvenChildren(LibraryTree tree) {
    if(tree == null) return 0;
    List<LibraryTree> childs = tree.getChildren();
    int count = (childs.size()%2 == 0) ? 1 : 0;
    for(LibraryTree c : childs) {
      count += countNodesEvenChildren(c);
    }
    return count;
  }
}

```
