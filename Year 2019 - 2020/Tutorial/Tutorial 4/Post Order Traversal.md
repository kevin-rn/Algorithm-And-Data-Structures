Implement a method postOrder(BinaryTree tree) that returns a list (for example a LinkedList) of all keys in the given tree, in post-order.

A binary tree can have at most two children, which are both again a binary tree (or null if the child does not exist).

The class BinaryTree can be found in the visible Library code. In case you want to work in Eclipse, you can copy this class to Eclipse as well.

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

### Library
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
    this(key);
    setLeft(left);
    setRight(right);
  }

  /**
   * @return The key of this BinaryTree node.
   */
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

  /**
   * @return true iff this BinaryTree node has a left child, false otherwise.
   */
  public boolean hasLeft() {
    return left != null;
  }

  /**
   * @return true iff this BinaryTree node has a right child, false otherwise.
   */
  public boolean hasRight() {
    return right != null;
  }

  /**
   * @param left
   *     The BinaryTree node to set as left child.
   */
  public void setLeft(BinaryTree left) {
    this.left = left;
  }

  /**
   * @param right
   *     The BinaryTree node to set as right child.
   */
  public void setRight(BinaryTree right) {
    this.right = right;
  }

  @Override
  public String toString() {
    return "BinaryTree{" + key + '}';
  }
}
```

### Solution
```java
import java.util.*;

class Solution {

  /**
   * @param tree
   *     The input BinaryTree.
   * @return A list of all keys in the tree, in post-order.
   */
  public static List<Integer> postOrder(BinaryTree tree) {
    List<Integer> result = new ArrayList<>();
    if (tree == null) return result;
    if (tree.hasLeft()) result.addAll(postOrder(tree.getLeft()));
    if (tree.hasRight()) result.addAll(postOrder(tree.getRight()));
    result.add(tree.getKey());
    return result;
  }
}
```
