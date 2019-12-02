You and your friends are planning to create a list of your favorite movies in a descending order, you decide to use Nodes.

A node stores an element as the value representing this node, as well as a reference to another node. In our case, the element of a node will be the name of a movie and the next node will be a reference to the node of the movie that comes next in the ranking.

Create an implementation for the empty methods in the Node class provided.

```java
class Node {

  // Each node object has these two fields
  private String element;

  private Node next;

  /**
   * Constructor
   * @param e - the element (value) stored in this node
   * @param next - the node that is next (i.e. our node refers to the next node)
   */
  public Node(String e, Node next) {
    this.element = e;
    this.next = next;
  }

  /**
   * Sets the element of this node with a new value
   * @param e - new value for this node
   */
  public void setElement(String e) {
    this.element = e;
  }

  /**
   * @return the element stored in this node
   */
  public String getElement() {
    return element;
  }

  /**
   * Sets the next node
   * @param next - the new node that our node refers to
   */
  public void setNext(Node next) {
    this.next = next;
  }

  /**
   * @return the next node
   */
  public Node getNext() {
    return next;
  }
}



```
