### Check whether search tree has height-balance property  

#### NOT the same as Binary tree completeness  

Implement a method that checks whether a binary tree has the height-balance property.
This property is defined as follows: for every internal node n of the tree, the heights of the children of n may differ by at most 1.

The binary tree can have at most two children, which are both again a binary tree (or null if the child does not exist).

The class BinaryTree has the following methods:
```java
class BinaryTree {
  // Constructor with no children
  BinaryTree(int key)

  // Constructor with two children
  BinaryTree(int key, BinaryTree left, BinaryTree right)

  // Returns the key of the root of this tree.
  int getKey();

  // Returns the left child of this tree iff hasLeft(v) is true, else null.
  BinaryTree getLeft();

  // Returns the right child of this tree iff hasRight(v) is true, else null.
  BinaryTree getRight();

  // Returns true iff this tree has a left child.
  boolean hasLeft();

  // Returns true iff this tree has a right child.
  boolean hasRight();

  // Set the new left child of this tree.
  void setLeft(BinaryTree child);

  // Set the new right child of this tree.
  void setRight(BinaryTree child);
}
```

### Template:
```java
class Solution {
  /**
   * This method checks whether the given tree has the height-balance property.
   *
   * @param tree
   *     the tree to check.
   * @return true iff the tree has the height-balance property, false otherwise.
   */
  public static boolean isTreeBalanced(BinaryTree tree) {
    // TODO
  }
}
```

### Test:
```
import static org.junit.Assert.*;
import org.junit.*;

public class UTest {

  @Test
  public void testEmptyTree() {
    assertTrue(Solution.isTreeBalanced(null));
  }

  @Test
  public void testOneLevel() {
    BinaryTree tree = new BinaryTree(42, new BinaryTree(84), new BinaryTree(21));
    assertTrue(Solution.isTreeBalanced(tree));
  }

  @Test
  public void testLinearTree() {
    assertFalse(Solution.isTreeBalanced(new BinaryTree(1, new BinaryTree(2, new BinaryTree(3), null), null)));
  }
}

```

____________________________________________________________________________________________________________________________

### Solution:
```java
class Solution {
  /**
   * This method checks whether the given tree has the height-balance property.
   *
   * @param tree
   *     the tree to check.
   * @return true iff the tree has the height-balance property, false otherwise.
   */
  public static boolean isTreeBalanced(BinaryTree tree) {
      return (tree == null) || (isTreeBalanced(tree.getLeft()) &&  isTreeBalanced(tree.getRight()) &&
            Math.abs(getHeight(tree.getLeft()) - getHeight(tree.getRight())) <= 1);
  }

  public static int getHeight(BinaryTree tree) {
    if(tree == null) return 0;
    int left = getHeight(tree.getLeft());
		int right = getHeight(tree.getRight());
		if (left == -1 || right == -1) return -1;
		if (Math.abs(left - right) > 1) return -1;
		return Math.max(left, right) + 1;
  }

}
```
