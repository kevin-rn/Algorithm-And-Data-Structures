### Search Tree
In this assignment you have to implement a method with the following signature:
Entry higherEntry(BinarySearchTree tree, int k)

The method higherEntry returns:

    the entry in the tree with the smallest key that is strictly greater than the given k, if it exists.
    or null, if the input is null, or if no entry can be found that satisfies the condition above.

We provide an implementation of the classes BinarySearchTree and Entry in the visible library code. They have the following methods:

```java
class BinarySearchTree {
  BinarySearchTree(int key, int value);
  BinarySearchTree(int key, int value, BinarySearchTree left, BinarySearchTree right);

  Entry getEntry();
  int getKey();
  int getValue();

  BinarySearchTree getLeft();
  BinarySearchTree getRight();

  boolean hasLeft();
  boolean hasRight();

  boolean setLeft(BinarySearchTree left);
  boolean setRight(BinarySearchTree right);
}

class Entry {
  Entry(int key, int value);
}
```

The binary search tree of class BinarySearchTree is not guaranteed to be balanced.

### Template: 
```java
import java.util.*;
class Solution {
  /**
   * Given a Binary Search Tree and an Integer, returns the Entry in this tree
   * with the smallest key that is strictly larger than k.
   *
   * @param tree
   *     Binary search tree to search in.
   * @param k
   *     The key of the resulting entry should be strictly larger than this k.
   * @return The entry with smallest key, strictly larger than k.
   */
  static Entry higherEntry(BinarySearchTree tree, int k) {
    // TODO
  }
}

```

### Library:
```java
class BinarySearchTree {
  private Entry entry;
  private BinarySearchTree left, right;

  /**
   * Simple constructor.
   *
   * @param key
   *     to set as key.
   */
  public BinarySearchTree(int key, int value) {
    this.entry = new Entry(key, value);
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
  public BinarySearchTree(int key, int value, BinarySearchTree left, BinarySearchTree right) {
    this.entry = new Entry(key, value);
    setLeft(left);
    setRight(right);
  }

  /**
   * @return Entry stored at this node
   */
  public Entry getEntry() {
    return entry;
  }

  /**
   * @return Key of the entry stored at this node
   */
  public int getKey() {
    return entry.key;
  }

  /**
   * @return Value of the entry stored at this node
   */
  public int getValue() {
    return entry.value;
  }

  /**
   * @return the left child.
   */
  public BinarySearchTree getLeft() {
    return left;
  }

  /**
   * @return the right child.
   */
  public BinarySearchTree getRight() {
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
  public void setLeft(BinarySearchTree left) {
    this.left = left;
  }

  /**
   * @param right
   *     to set
   */
  public void setRight(BinarySearchTree right) {
    this.right = right;
  }
}

class Entry {
  public final int key;
  public final int value;

  public Entry(int key, int value) {
    this.key = key;
    this.value = value;
  }
}

```

### Test:
```java
import org.junit.*;

import static org.junit.Assert.*;

public class UTest {
  @Test
  public void testBase() {
    BinarySearchTree tree = new BinarySearchTree(1, 42);
    assertEquals(1, Solution.higherEntry(tree, 0).key);
    assertNull(Solution.higherEntry(tree, 1));
    assertNull(Solution.higherEntry(tree, 2));
    assertNull(Solution.higherEntry(null, 42));
  }

  @Test
  public void testSmall() {
    BinarySearchTree tree = new BinarySearchTree(42, 42, new BinarySearchTree(21, 21, new BinarySearchTree(10, 10), new BinarySearchTree(30, 30)), new BinarySearchTree(84, 84, new BinarySearchTree(60, 60), new BinarySearchTree(100, 100)));
    assertEquals(10, Solution.higherEntry(tree, 2).key);
    assertEquals(60, Solution.higherEntry(tree, 42).key);
    assertEquals(100, Solution.higherEntry(tree, 88).key);
  }
}


```

________________________________________________________________________________________________________________________

### Solution:
```java

class Solution {
  /**
   * Given a Binary Search Tree and an Integer, returns the Entry in this tree
   * with the smallest key that is strictly larger than k.
   *
   * @param tree
   *     Binary search tree to search in.
   * @param k
   *     The key of the resulting entry should be strictly larger than this k.
   * @return The entry with smallest key, strictly larger than k.
   */
  static Entry higherEntry(BinarySearchTree tree, int k) {
      if (tree == null) return null;
      BinarySearchTree current = tree, ans = null; 
      while (current != null) { 
        if (current.getKey() > k) { 
          ans = current; 
          current = current.getLeft(); 
        } else current = current.getRight(); 
      } 
      if (ans != null) return ans.getEntry(); 
      return null; 
    }
}


```
