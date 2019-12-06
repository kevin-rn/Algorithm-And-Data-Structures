In this exercise, you need to complete the implementation of a class defining a singly-linked list, SLList, based on the given skeleton code.

This skeleton already contains the implementation of a class Node. Each Node object has an element and a pointer to the next Node. 
Implementations of methods setElement, getElement, setNext, and getNext are also provided. You are encouraged to inspect the comments in the definition of this class to understand the structure.

Following the definition of class Node, we have provided you the skeleton of class SLList. 
The getFirst method is already implemented. 
You are expected to complete the implementation of this class by completing following methods:

  addFirst
  removeFirst
  zip
  append
  dropEven

You can check the comments in the code to see what each method is expected to implement.

IMPORTANT: You are not allowed to add extra class fields to any of the classes. 
If you do add extra class fields, points may be deducted.

### Library
```java
import java.util.*;

class Pair<A, B> {
  private A a;
  private B b;

  public Pair(A a, B b) {
    this.a = a;
    this.b = b;
  }

  public A getA() {
    return a;
  }

  public B getB() {
    return b;
  }

  @Override
  public boolean equals(Object o) {
    if (this == o)
      return true;
    if (o == null || getClass() != o.getClass())
      return false;
    Pair<?, ?> pair = (Pair<?, ?>) o;
    return Objects.equals(a, pair.a) && Objects.equals(b, pair.b);
  }

  @Override
  public String toString() {
    return "Pair{" + a + ", " + b + '}';
  }
}
```

### Solution
```java
class SLList<T> {
  class Node {
    // Each Node object has these two fields
    private T element;
    private Node next;

    // Constructor: Creates a Node object with element = e and next = n
    Node(T e, Node n) {
      element = e;
      next = n;
    }

    // This function gets T e as input and sets e as the element of the Node
    public void setElement(T e) {
      element = e;
    }

    // This function returns the element variable of the Node
    public T getElement() {
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
   * @return The element in the first Node of this SLL. If the list is empty, this method returns null.
   */
  public T getFirst() {
    if (head == null)
      return null;
    return head.getElement();
  }

  /**
   * Adds element e in a new Node to the head of the list.
   *
   * @param e
   *     The element to add.
   */
	public void addFirst(T e) {
		if (e != null) {
			Node n = new Node(e, head);
			this.head = n;
		}
	}

  /**
   * Remove the first Node in the list and return its element.
   *
   * @return The element of the first Node. If the list is empty, this method returns null.
   */
	public T removeFirst() {
		if (head == null) return null;
		Node res = head;
		head = head.getNext();
		return res.getElement();
	}

  /**
   * Combine this list with the other list.
   * Each element of the resulting list is a Pair object holding one element of this list
   * and the corresponding element at the same position of the other list.
   * If one list is longer than the other, any extra elements should be dropped.
   * Example: Zipping [1, 2] with [5, 6, 7] results in [(1, 5), (2, 6)], where (x, y) denotes a Pair object.
   *
   * @param other
   *     The other list to combine elements with. Is treated as an empty list if it is null.
   * @return A new list with alternated elements of this list and the other list.
   */
	public SLList<Pair<T, T>> zip(SLList<T> other) {
		if (other == null) return new SLList<Pair<T, T>>();
		T left = this.removeFirst();
		T right = other.removeFirst();
		SLList<Pair<T, T>> temp = new SLList<Pair<T, T>>();
		
		while (left != null && right != null) {
			temp.addFirst(new Pair<T, T>(left, right));
			left = this.removeFirst();
			right = other.removeFirst();
		}
		
		SLList<Pair<T, T>> res = new SLList<Pair<T, T>>();
		Pair<T, T> n = temp.removeFirst();
		while(n != null && n.getA() != null && n.getB() != null) {
			res.addFirst(n);
			n = temp.removeFirst();
		}
		return res;
	}
 

  /**
   * Appends another SLL to this SLL.
   *
   * @param other
   *     The list to append to this list. Is treated as an empty list if it is null.
   */
	public void append(SLList<T> other) {
		if (this.head == null) {
			this.head = other.head;
			return;
		}
		if (other == null) return;
		
		Node prev = null;
		Node curr = this.head;
		
		while(curr != null) {
			prev = curr;
			curr = curr.getNext();
		}
		
		prev.setNext(other.head);
	}

  /**
   * Removes all elements at the even positions in this list.
   * Note that the head of the list is element number 0, which is an even position.
   */
	public void dropEven() {
		if (this == null || this.head == null) return;
		if (head.getNext() == null) {
		  removeFirst();
		  return;
		}
		
		head = head.getNext();
		Node temp = head;
		
		while (temp != null && temp.getNext()!= null) {
		  temp.setNext(temp.getNext().getNext());
		  temp = temp.getNext();
		}
	}
}
```
