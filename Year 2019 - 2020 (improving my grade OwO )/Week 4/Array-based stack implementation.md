### Array-based stack implementation

Implement the class ArrayStack using an array. The other fields of the class are used as follows:

    capacity keeps track of the allocated space.
    size keeps track of the number of elements in the stack.

In this question we have provided you with a skeleton of the class ArrayStack. You are expected to complete the implementation by completing the following methods:

    ArrayStack()
    size()
    isEmpty()
    isFull()
    peek()
    push(Object o)
    pop()
    toString()

You can check the comments in the code to see what each method is expected to implement.

IMPORTANT: You MAY NOT use the function arraycopy from System, Arrays or similar. In an exam setting, your grade would be overridden to 1 if you do use library functions to copy arrays.

IMPORTANT: pay special attention to pop: if removing top would make the stack use strictly less than (i.e. <) 25% of its capacity, then the capacity is halved, with a minimum capacity of 1. This is enforced by the specification tests.

```java

class ArrayStack {
  private Object[] elements;
  private int size;
  private int capacity;

  /**
   * Creates an empty ArrayStack with capacity 1.
   */
  public ArrayStack() {
    capacity = 1;
    elements = new Object[capacity];
    size = 0;
  }

  /**
   * @return The size of this ArrayStack.
   */
  public int size() {
    return size;
  }

  /**
   * @return `true` iff this ArrayStack is empty, `false` otherwise.
   */
  public boolean isEmpty() {
    return size == 0;
  }

  /**
   * @return `true` iff the size is equal to the capacity, `false` otherwise.
   */
  public boolean isFull() {
    return size == capacity;
  }

  /**
   * @return the top element of the stack without removing it
   */
  public Object peek() throws EmptyStackException {
    if(this.isEmpty()) throw new EmptyStackException();
    return elements[size-1];
  }

  /**
   * Adds `o` to the stack.
   * If capacity of stack was too small, capacity is doubled and `o` is added.
   *
   * @param o
   *     the element to add to the stack.
   */
  public void push(Object o) {
    if(this.isFull()) {
      capacity *= 2;
      Object[] replace = new Object[capacity];
      for(int i = 0; i < size; i++){
        replace[i] = elements[i];
      }
      elements = replace;
    }
    elements[size] = o;
    size++;
  }

  /**
   * Removes the top element from the stack.
   * If removing top would make the stack use less than 25% of its capacity,
   * then the capacity is halved.
   *
   * @return the element which was at the top of the stack.
   * @throws EmptyStackException
   *     iff the queue is empty
   */
  public Object pop() throws EmptyStackException {
    if(this.isEmpty()) throw new EmptyStackException();
    Object o = elements[size-1];
    if(this.size() == (capacity/4)){
      capacity /= 2;
      Object[] replace = new Object[capacity];
      for(int i = 0; i < size; i++){
        replace[i] = elements[i];
      }
      elements = replace;
    }
    size--;
    return o;
  }

  /**
   * @return a String representation of the ArrayStack
   * Example output for ArrayStack with 2 elements and capacity 5:
   * <ArrayStack[1,2]>(Size=2, Cap=5)
   */
  public String toString() {
    StringBuilder str = new StringBuilder();
    str.append("<ArrayStack[");
    for(int i =0; i< this.size(); i++){
      if(i+1 == size) {
        str.append(elements[i]);
      } else str.append(elements[i] + ",");
    }
    str.append("]>(Size=" + size + ", Cap=" + capacity + ")");
    return str.toString();
  }

  // For testing, do not remove or change.
  public Object[] getElements() {
    return elements;
  }
}
```
