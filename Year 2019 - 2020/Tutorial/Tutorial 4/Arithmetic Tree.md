An arithmetic expression like:
(3+1)

can be represented using a binary tree. Each leaf in this tree will be a constant integer value and each internal node will be a operator of the expression. For example, the expression
(3+1)
can represented using the following binary tree:
   +
  / \
 /   \
3     1

The root contains the operator +, the left leaf contains the constant 3, and the right leaf contains the constant 1.

In this exercise you need to implement the eval method, which takes as input a binary arithmetic tree and outputs the result of the arithmetic expression.

The only operators allowed in this binary arithmetic tree are: +, -, and *.

### Library
```java
package weblab;

abstract class Node<T> {
  public T val;
}

/**
 * Internal Node that stores an operator represented as a string
 */
 @SuppressWarnings("rawtypes")
class InternalNode extends Node<String> {
  public Node left;
  public Node right;

  public InternalNode(String operator, Node left, Node right) {
    this.val = operator;
    this.left = left;
    this.right = right;
  }
}

/**
 * Leaf Node that stores an operand represented as an integer
 */
class LeafNode extends Node<Integer> {
  public LeafNode(int constant) {
    this.val = constant;
  }
}
```

### Solution
```java
package weblab;

class Solution {
  /**
   * Evaluates the arithmetic expression stored in this binary tree.
   *
   * @param node
   * @return
   * @throws IllegalArgumentException
   */
   @SuppressWarnings("rawtypes")
  public static int eval(Node node) throws IllegalArgumentException {
    if (node instanceof LeafNode) return (int) node.val;
    InternalNode internalNode = (InternalNode) node;
    switch (internalNode.val) {
      case "+": return eval(internalNode.left) + eval(internalNode.right);
      case "-": return eval(internalNode.left) - eval(internalNode.right);
      case "*": return eval(internalNode.left) * eval(internalNode.right);
      default: throw new IllegalArgumentException();
    }
  }
}

```
