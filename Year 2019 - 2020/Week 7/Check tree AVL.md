### Check tree AVL
Implement a method that checks whether a binary tree is an AVL tree without duplicate values.

The binary tree can have at most two children, which are both again a binary tree (or null if the child does not exist).

A binary tree is an AVL tree when:

    The tree is a binary search tree.
    The difference between the heights of two subtrees of any node is not larger than 1.

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

### Template:
```java
class Solution {

  /**
   * Computes whether the BinaryTree is an AVL tree.
   *
   * @param tree
   *     the BinaryTree to check.
   * @return true iff the BinaryTree is an AVL tree, else false.
   */
  public static boolean isTreeAVL(BinaryTree tree) {
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
import org.junit.*;

public class UTest {

  @Test
  public void testJustRoot() {
    BinaryTree tree = new BinaryTree(42);
    assertTrue(Solution.isTreeAVL(tree));
  }

  @Test
  public void testOneLevelTrue() {
    BinaryTree tree = new BinaryTree(42, new BinaryTree(21), new BinaryTree(84));
    assertTrue(Solution.isTreeAVL(tree));
  }

  @Test
  public void testOneLevelFalse() {
    BinaryTree tree = new BinaryTree(42, new BinaryTree(84), new BinaryTree(21));
    assertFalse(Solution.isTreeAVL(tree));
  }

  @Test
  public void testOneLevelFalseDuplicate() {
    BinaryTree tree = new BinaryTree(42, new BinaryTree(42), new BinaryTree(21));
    assertFalse(Solution.isTreeAVL(tree));
  }

  @Test
  public void testOneLeftChild() {
    BinaryTree tree = new BinaryTree(42, new BinaryTree(21), null);
    assertTrue(Solution.isTreeAVL(tree));
    tree = new BinaryTree(42, new BinaryTree(84), null);
    assertFalse(Solution.isTreeAVL(tree));
  }

  /*
         42
        /
       36
      /  \
     21  39
   */
  @Test
  public void testTwoLevelsSkew2() {
    BinaryTree tree = new BinaryTree(42, new BinaryTree(36, new BinaryTree(21), new BinaryTree(39)), null);
    assertFalse(Solution.isTreeAVL(tree));
  }
}


```

__________________________________________________________________________________________________

### Solution:
```java
class Solution {

  /**
   * Computes whether the BinaryTree is an AVL tree.
   *
   * @param tree
   *     the BinaryTree to check.
   * @return true iff the BinaryTree is an AVL tree, else false.
   */
  public static boolean isTreeAVL(BinaryTree tree) {
    if (tree == null) return true; 
    int lh = height(tree.getLeft()), rh = height(tree.getRight()); 
  
    if (Math.abs(lh - rh) <= 1 && isTreeAVL(tree.getLeft()) && isTreeAVL(tree.getRight())) 
        return bst(tree, Integer.MIN_VALUE, Integer.MAX_VALUE);
    else return false; 
  }

  public static int height(BinaryTree tree) {
     if (tree == null) return 0; 
     return 1 + Math.max(height(tree.getLeft()), height(tree.getRight())); 
  }
  
  public static boolean bst(BinaryTree tree, int min, int max) {
    if(tree == null) return true;
    if(tree.getKey() < min || tree.getKey() > max) return false;
    return bst(tree.getLeft(), min, tree.getKey()-1) && bst(tree.getRight(), tree.getKey() + 1, max);
  }

}


```
