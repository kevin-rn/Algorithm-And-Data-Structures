In this assignment you have to implement the method countNodesAtLevel, which counts the number of non-null nodes at a given level of a binary tree.

The method takes as input a binary tree of type BinaryTree and an integer value denoting the level, and should return the number of nodes found at the given level in the given binary tree.

The method should return 0, if the tree is null.

In the library you can find an implementation of the class BinaryTree.

### Template:
```java
class Solution {
  /**
   * Counts the number of nodes in the tree at a certain level.
   *
   * @param tree
   *     The binary tree to count nodes in.
   * @param level
   *     The specified level to count nodes in.
   * @return the number of nodes at that level, or 0 if tree is null.
   */
  public static int countNodesAtLevel(BinaryTree tree, int level) {
    // TODO
  }
}

```

### Library:
```java
class BinaryTree {

  private int key;

  private BinaryTree left, right;

  /**
   * Simple constructor.
   *
   * @param key
   *     to set as key.
   */
  public BinaryTree(int key) {
    this.key = key;
  }

  /**
   * Extended constructor.
   *
   * @param key
   *     to set as key.
   * @param left
   *     to set as left child.
   * @param right
   *     to set as right child.
   */
  public BinaryTree(int key, BinaryTree left, BinaryTree right) {
    this.key = key;
    this.left = left;
    this.right = right;
  }

  public int getKey() {
    return key;
  }

  /**
   * @return the left child.
   */
  public BinaryTree getLeft() {
    return left;
  }

  /**
   * @return the right child.
   */
  public BinaryTree getRight() {
    return right;
  }

  public boolean hasLeft() {
    return left != null;
  }

  public boolean hasRight() {
    return right != null;
  }
}

```

### Test:
```java
import static org.junit.Assert.*;

import org.junit.*;

public class UTest {
  @Test
  public void testSmall() {
    BinaryTree tree = new BinaryTree(0, new BinaryTree(1, new BinaryTree(3), new BinaryTree(4)), new BinaryTree(2, new BinaryTree(5), new BinaryTree(6)));
    assertEquals(1, Solution.countNodesAtLevel(tree, 0));
    assertEquals(2, Solution.countNodesAtLevel(tree, 1));
    assertEquals(4, Solution.countNodesAtLevel(tree, 2));
  }

  @Test
  public void testNull() {
    BinaryTree tree = null;
    assertEquals(0, Solution.countNodesAtLevel(tree, 0));
  }
}
```


_______________________________________________________________________________________________________________
### Solution:
```java
class Solution {
  /**
   * Counts the number of nodes in the tree at a certain level.
   *
   * @param tree
   *     The binary tree to count nodes in.
   * @param level
   *     The specified level to count nodes in.
   * @return the number of nodes at that level, or 0 if tree is null.
   */
  public static int countNodesAtLevel(BinaryTree tree, int level) {
    if(tree == null) return 0;
    if(level == 0) return 1;
    return countNodesAtLevel(tree.getLeft(), level-1) + countNodesAtLevel(tree.getRight(), level-1);
  }
}
```
