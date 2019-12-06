In this exercise we have a non-binary tree.  
This means that the tree can have as many children as it needs (or, more formally, anywhere between 0 and n children).  
You can find the implementation of this tree in the library.

You will need to implement a method that performs traversal of this tree using breadth-first search (BFS).

#### Library
```java
class Tree {

  private int key;

  private List<Tree> children;

  /**
   * Constructor without children
   * @param key - the key of the root
   */
  public Tree(int key) {
    this.key = key;
    this.children = new ArrayList<>();
  }

  /**
   * Constructor with children
   * @param key - the key of the root
   * @param children - a list of all the children
   */
  public Tree(int key, List<Tree> children) {
    this.key = key;
    this.children = children;
  }

  /**
   * @return the key of the root of this tree
   */
  public int getKey() {
    return this.key;
  }

  /**
   * @return the children of the root of this tree
   */
  public List<Tree> getChildren() {
    return this.children;
  }

  /**
   * Add a children (subtree with one or more nodes) to this tree.
   * @param tree - the tree that needs to be added
   */
  public void addChildren(Tree tree) {
    this.children.add(tree);
  }
}

```


### Solution
```java
import java.util.*;

class Solution {

  /**
   * Traverses the tree in a breadth first search order. The result will be a list containing the key of each node in the correct order.
   *
   * @param tree - the tree that will be traversed
   * @return list containing the keys of each node in the correct order
   */
  public static List<Integer> bfs(Tree tree) {
    List<Integer> list = new ArrayList<Integer>();
    if(tree == null) return list;
    Queue<Tree> q = new LinkedList<>();
    q.add(tree);
    while(!q.isEmpty()) {
      Tree current = q.poll();
      list.add(current.getKey());
      if(current.getChildren() != null) q.addAll(current.getChildren());
      }
    return list;
  }
}
```
