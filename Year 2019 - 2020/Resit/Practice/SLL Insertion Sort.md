
Implement the method SLList insertionSort(SLList list), which performs insertion sort on the given singly linked list of class SLList. The method should return a new singly linked list with the elements of the original list in non-decreasing order.

In the case that the input list is null, you should return null.

We provide an implementation of the classes SLList class and its inner class Node in the visible library code. They have the following methods:
```java
class SLList {
  SLList();
  SLList(int... elements);

  Node getFirst();
  void addFirst(int e);
  int removeFirst();

  void addAfter(Node node, int e);

  boolean equals(Object o);
  String toString();

  class Node {
    Node(int e, Node n);

    void setElement(int e);
    int getElement();

    void setNext(Node n);
    Node getNext();
  }
}
```
Hint: use SLList.Node to refer to the Node class, instead of Node.

IMPORTANT: Your implementation will need to satisfy the following requirements:

    You are not allowed to use any data structures other than the SLList class that we provide.
    Your implementation must use insertion sort, and not any other sorting algorithm.
    The worst-case time complexity of your implementation needs to be O(n2) where n is the size of the singly linked list.
    
### Template:
```java
class Solution {
  /**
   * @param list
   *     The singly linked list to sort.
   * @return A new singly linked list that contains the elements as the input list sorted in non-decreasing order.
   */
  static SLList insertionSort(SLList list) {
    // TODO
  }
}

```

### Library:
```java
import java.util.*;

class SLList {
  class Node {
    // Each Node object has these two fields
    private int element;
    private Node next;

    // Constructor: Creates a Node object with element = e and next = n
    Node(int e, Node n) {
      element = e;
      next = n;
    }

    // This function gets int e as input and sets e as the element of the Node
    public void setElement(int e) {
      element = e;
    }

    // This function returns the element variable of the Node
    public int getElement() {
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

  public SLList(int... elements) {
    LinkedList<Integer> reversed = new LinkedList<>();
    for (int element : elements) {
      reversed.add(element);
    }
    while (!reversed.isEmpty()) {
      this.addFirst(reversed.removeLast());
    }
  }

  /**
   * @return The element in the first Node of this SLL. If the list is empty, this method returns null.
   */
  public Node getFirst() {
    if (head == null)
      return null;
    return head;
  }

  /**
   * Adds element e in a new Node to the head of the list.
   *
   * @param e
   *     The element to add.
   */
  public void addFirst(int e) {
    head = new Node(e, head);
  }

  /**
   * Remove the first Node in the list and return its element.
   *
   * @return The element of the first Node.
   * @throws NullPointerException
   *     If the list is empty.
   */
  public int removeFirst() {
    Node result = head;
    head = head.getNext();
    return result.getElement();
  }

  /**
   * Adds an element after an already existing node.
   *
   * @param node
   *     The node to add a new element after.
   * @param e
   *     The new element to add.
   */
  public void addAfter(Node node, int e) {
    Node newNode = new Node(e, node.getNext());
    node.setNext(newNode);
  }

  @Override
  public boolean equals(Object o) {
    if (this == o)
      return true;
    if (o == null || getClass() != o.getClass())
      return false;
    SLList slList = (SLList) o;
    Node a = this.head;
    Node b = slList.head;
    while (a != null && b != null) {
      if (!Objects.equals(a.getElement(), b.getElement())) {
        return false;
      }
      a = a.next;
      b = b.next;
    }
    return Objects.equals(a, b);
  }

  @Override
  public String toString() {
    StringBuilder sb = new StringBuilder();
    sb.append("SLList[");
    Node current = this.head;
    while (current != null) {
      sb.append(current.getElement());
      sb.append(",");
      current = current.next;
    }
    sb.replace(sb.length() - 1, sb.length(), "]");
    return sb.toString();
  }
}

```

### Test:
```java
import org.junit.*;

import static org.junit.Assert.*;

public class UTest {
  @Test
  public void testEmpty() {
    SLList input = new SLList();
    SLList output = new SLList();
    assertEquals(output, Solution.insertionSort(input));
  }

  @Test
  public void testNull() {
    assertNull(Solution.insertionSort(null));
  }

  @Test
  public void testExample() {
    SLList input = new SLList(3, 1, 2);
    SLList output = new SLList(1, 2, 3);
    assertEquals(output, Solution.insertionSort(input));
  }
}
```

___________________________________________________________________________________________________________________
### Solution:
```java
class Solution {
  /**
   * @param list
   *     The singly linked list to sort.
   * @return A new singly linked list that contains the elements as the input list sorted in non-decreasing order.
   */
 static SLList insertionSort(SLList list) { 
    SLList result = new SLList();
    if (list == null) return null; 
    else if (list.getFirst() == null) return result; 
    SLList.Node current = list.getFirst(), index = null; 
    while (current != null) { 
      index = current.getNext(); 
      while(index != null) { 
        if (current.getElement() > index.getElement()) { 
          int temp = current.getElement(); 
          current.setElement(index.getElement()); 
          index.setElement(temp); 
        }
      index = index.getNext(); 
      }
    current = current.getNext(); 
    }
    result.addFirst(list.getFirst().getElement());
    for(SLList.Node next = list.getFirst().getNext(), r = result.getFirst(); next != null; r = r.getNext(), next = next.getNext()) {
      result.addAfter(r, next.getElement());
    }
    
    return result; 
  }
}
```
