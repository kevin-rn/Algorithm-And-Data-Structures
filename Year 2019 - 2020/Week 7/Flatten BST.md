### Flatten BST
Implement a method that checks return all values in a given Binary Search Tree in descending order. Besides the list of all values, the method can only use O(h) space, where h is the height of the tree. Furthermore the method must run in O(n) time, where n

is the amount of nodes in the tree.

The binary tree can have at most two children, which are both again a binary tree (or null if the child does not exist).

The class BinaryTree has the following methods:

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

IMPORTANT: In an exam setting, your grade for this exercise would be overridden to 1 if your algorithm does not run in O(n)
time or uses more than O(h) space.
If you want to be sure your implementation satisfies the requirements, ask a TA for feedback during the lab.

### Template:
```java
import java.util.*;

class Solution {

  /**
   * Return all elements in the given BST in descending order.
   * @param tree The BST to traverse.
   * @return A list of all elements in reverse order.
   */
  public static List<Integer> descendingOrder(BinaryTree tree) {
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
  public void testOneLevel() {
    BinaryTree tree = new BinaryTree(42, new BinaryTree(21), new BinaryTree(84));
    assertEquals(Arrays.asList(84, 42, 21), Solution.descendingOrder(tree));
  }

  @Test
  public void testOneLeftChild() {
    BinaryTree tree = new BinaryTree(42, new BinaryTree(21), null);
    assertEquals(Arrays.asList(42, 21), Solution.descendingOrder(tree));
  }
}

```

_______________________________________________________________________________________________________________________
### Solution:
```java
import java.util.*;

class Solution {


  /**
   * Return all elements in the given BST in descending order.
   * @param tree The BST to traverse.
   * @return A list of all elements in reverse order.
   */
  public static List<Integer> descendingOrder(BinaryTree tree) {
      if(tree == null) return null;
      LinkedList<Integer> list = new LinkedList<Integer>();
      flat(list, tree);
      return list;
  }
  
  public static void flat(LinkedList<Integer> list, BinaryTree tree) {
    if(tree != null) {
      flat(list, tree.getLeft());
      list.addFirst(tree.getKey());
      flat(list, tree.getRight());
    }
  }
}
```


