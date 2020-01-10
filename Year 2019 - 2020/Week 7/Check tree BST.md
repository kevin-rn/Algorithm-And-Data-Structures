###  Check tree BST
Implement a method that checks whether a binary tree is a binary search tree without duplicate values. This method must run in O(n) time, where n

is the amount of nodes in the tree.

The binary tree can have at most two children, which are both again a binary tree (or null if the child does not exist).

The class BinaryTree has the following methods:
```java
class BinaryTree {
  // Constructor with no children
  BinaryTree(int key);

  // Constructor with two children
  BinaryTree(int key, BinaryTree left, BinaryTree right);

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
IMPORTANT: In an exam setting, your grade for this exercise would be overridden to 1 if your algorithm does not run in O(n)
time.
To help you test this, there is one spec-test for the runtime of your method. This test is worth 10/100 points. Note that adding many debug prints may also trigger a timeout of this test. If you want to be sure your implementation satisfies the requirement, ask a TA for feedback during the lab.

### Template:
```java
import java.util.*;

class Solution {

  /**
   * Computes whether the BinaryTree is a binary search tree.
   *
   * @param tree
   *     the BinaryTree to check.
   * @return true iff the BinaryTree is a binary search tree, else false.
   */
  public static boolean isTreeBST(BinaryTree tree) {
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
    setLeft(left);
    setRight(right);
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

  /**
   * @param left
   *     to set
   */
  public void setLeft(BinaryTree left) {
    this.left = left;
  }

  /**
   * @param right
   *     to set
   */
  public void setRight(BinaryTree right) {
    this.right = right;
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
  public void testOneLevelTrue() {
    BinaryTree tree = new BinaryTree(42, new BinaryTree(21), new BinaryTree(84));
    assertTrue(Solution.isTreeBST(tree));
  }

  @Test
  public void testOneLevelFalse() {
    BinaryTree tree = new BinaryTree(42, new BinaryTree(84), new BinaryTree(21));
    assertFalse(Solution.isTreeBST(tree));
  }

  @Test
  public void testOneLevelFalseDuplicate() {
    BinaryTree tree = new BinaryTree(42, new BinaryTree(42), new BinaryTree(21));
    assertFalse(Solution.isTreeBST(tree));
  }

  @Test
  public void testOneLeftChild() {
    BinaryTree tree = new BinaryTree(42, new BinaryTree(21), null);
    assertTrue(Solution.isTreeBST(tree));
    tree = new BinaryTree(42, new BinaryTree(84), null);
    assertFalse(Solution.isTreeBST(tree));
  }
}


```

_________________________________________________________________________________________________________________-
### Solution:
```java
class Solution {

  /**
   * Computes whether the BinaryTree is a binary search tree.
   *
   * @param tree
   *     the BinaryTree to check.
   * @return true iff the BinaryTree is a binary search tree, else false.
   */
  public static boolean isTreeBST(BinaryTree tree) {
   return bst(tree, Integer.MIN_VALUE, Integer.MAX_VALUE);
  }
  
  public static boolean bst(BinaryTree tree, int min, int max) {
    if(tree == null) return true;
    if(tree.getKey() < min || tree.getKey() > max) return false;
    return bst(tree.getLeft(), min, tree.getKey()-1) && bst(tree.getRight(), tree.getKey() + 1, max);
  }
}


```
