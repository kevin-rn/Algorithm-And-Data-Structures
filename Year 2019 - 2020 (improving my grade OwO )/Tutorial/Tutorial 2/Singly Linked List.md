    Description
    Assignment Info

Now that you’ve got the nodes all sorted out, you would like to have some additional utility. For this you decide to create your film ranking using a Singly Linked List: a data structure that uses nodes to create a list. This could be very useful because sometimes you want to insert a film you’ve forgotten somewhere in the middle of the list, or reorder some of the films.

In this exercise, you need to complete the implementation of a class defining a singly-linked list, SLList, based on the given skeleton code.

This skeleton already contains the implementation of a class Node. Each Node object has an element and a pointer to the next Node. Implementations of methods getNext, getElement and setNext are also provided. You are encouraged to inspect the comments in the definition of this class to understand the structure.

Following the definition of class Node, we have provided you the skeleton of class SLList. You are expected to complete the implementation of this class by completing the following methods:

    addFirst
    removeFirst
    addLast
    removeLast
    removeFromPosition

You can check the comments in the code to see what each method is expected to implement.

```java
class SLList {

  class Node {

    // Each node object has these two fields
    private Object element;

    private Node next;

    // Constructor: Creates a Node object with element = e and next = n
    Node(Object e, Node n) {
      element = e;
      next = n;
    }

    // This function gets Object e as input and sets e as the element of the Node
    public void setElement(Object e) {
      element = e;
    }

    // This function returns the element variable of the Node
    public Object getElement() {
      return element;
    }

    // This function gets Node n as input and sets the next variable of the current Node object as n.
    public void setNext(Node n) {
      next = n;
    }

    // This function returns the next Node
    public Node getNext() {
      return next;
    }
  }

  // Each object in SLList has one field head, which points to the starting Node of SLList.
  private Node head;

  /**
   * Constructor: initialises the head field as null
   */
  public SLList() {
    head = null;
  }

  /**
   * @return The element in the head Node of the SLL
   */
  public Object getHead() {
    return head.getElement();
  }

  /**
   * Adds element e in a new Node to the head of the list.
   *
   * @param e The element to add.
   */
  public void addFirst(Object e) {
    head = new Node(e, head);
  }

  /**
   * Remove the first Node in the list and return its element.
   *
   * @return The element of the head Node. If the list is empty, this method returns null.
   */
  public Object removeFirst() {
    if (head == null) return null;
    Node n = head;
    head = head.getNext();
    return n.getElement();
  }

  /**
   * Adds element e in a new Node to the tail of the list.
   *
   * @param e
   *     The element to add.
   */
  public void addLast(Object e) {
    if (head == null) addFirst(e);
    else {
      Node n = new Node(e, null), m = head;
      while (m.getNext() != null) m = m.getNext();
      m.setNext(n);
    }
  }

  /**
   * Remove the last Node in the list and return its element.
   *
   * @return The element of the tail Node. If the list is empty, this method returns null.
   */
  public Object removeLast() {
    if (head == null) return null;
    if (head.getNext() == null) return removeFirst();
    Node m = head, n = head; 
    while (m.getNext() != null) {
      n = m;
      m = m.getNext();
    }
    n.setNext(null);
    return m.getElement();
  }

  /**
   * Remove Node at position pos and return its element.
   * The list is zero indexed, so the first element in the list corresponds to position 0.
   * This also means that `removeFromPosition(0)` has the same effect as `removeFirst()`.
   *
   * @param pos The position to remove the Node from.
   * @return The element of the Node in position pos. If there is no Node in position pos, this method returns null.
   */
  public Object removeFromPosition(int pos) {
    if (pos == 0) return removeFirst();
    if (pos < 0) return null;
    Node n = head, m = null; 
    while (pos > 0 && n != null) {
      m = n;
      n = n.getNext();
      pos--;
    }
    
    if (n == null) return null;
    m.setNext(n.getNext());
    return n.getElement();
  }
}
```
