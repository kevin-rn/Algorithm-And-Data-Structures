### Array-based Stack
In this exercise you have to implement a stack using an array of fixed length. The class ArrayBasedStack, has the following fields:

    stack, the array representing the stack.
    size, an integer representing the current number of items stored in the stack.

You have to implement the following methods:

    ArrayBasedStack, the constructor.
    push, which pushes a new element given as input onto the top of the stack. Returns the element if added to the stack successfully, or null if the stack is full.
    pop, which removes the top element from the stack. Returns the element at the top of the stack, or null if no element is found in the stack.
    peek, returns the top element from the stack (without removing it), or null if no element is found in the stack.

IMPORTANT: The stack has a fixed capacity, this means that you do not need to resize the array representing the stack.

### Template:
```java
class ArrayBasedStack {
  public Object[] stack;
  public int size;

  /**
   * The constructor of the ArrayBasedStack.
   *
   * @param capacity
   *     Maximum number of items that can be stored in the stack.
   */
  public ArrayBasedStack(int capacity) {
    // TODO
  }

  /**
   * Push an item to the stack.
   *
   * @param o
   *     Object that is pushed on the stack.
   * @return the object, iff the object has been pushed to stack successfully.
   * Returns null, if the object cannot be pushed to the stack.
   */
  public Object push(Object o) {
    // TODO
  }

  /**
   * Pops the first item from the stack.
   *
   * @return the object, iff the object has been popped from stack successfully. Null, if the stack is empty.
   */
  public Object pop() {
    // TODO
  }

  /**
   * Check the item on top of the stack, without removing it.
   *
   * @return the top object, iff the stack has an item. Null, if the stack is empty.
   */
  public Object peek() {
    // TODO
  }
}

```

### Test:
```java
import org.junit.*;

import static org.junit.Assert.*;

public class UTest {
  @Test
  public void testConstructor() {
    ArrayBasedStack stack = new ArrayBasedStack(3);
    assertEquals(3, stack.stack.length);
    assertEquals(0, stack.size);
    assertArrayEquals(new Object[3], stack.stack);
  }

  @Test
  public void testPush() {
    ArrayBasedStack stack = new ArrayBasedStack(2);
    assertEquals(5, stack.push(5));
    assertEquals(42, stack.push(42));
    assertNull(stack.push(512));
  }

  @Test
  public void testPop() {
    ArrayBasedStack stack = new ArrayBasedStack(4);
    assertNull(stack.pop());
    assertEquals(5, stack.push(5));
    assertEquals(5, stack.pop());
    assertNull(stack.pop());
  }

  @Test
  public void testPeek() {
    ArrayBasedStack stack = new ArrayBasedStack(4);
    assertNull(stack.peek());
    assertEquals(5, stack.push(5));
    assertEquals(5, stack.peek());
    assertEquals(5, stack.peek());
  }
}


```

__________________________________________________________________________________________________________________

### Solution:
```java
class ArrayBasedStack {
  public Object[] stack;
  public int size;

  /**
   * The constructor of the ArrayBasedStack.
   *
   * @param capacity
   *     Maximum number of items that can be stored in the stack.
   */
  public ArrayBasedStack(int capacity) {
    stack = new Object[capacity];
    size = 0;
  }

  /**
   * Push an item to the stack.
   *
   * @param o
   *     Object that is pushed on the stack.
   * @return the object, iff the object has been pushed to stack successfully.
   * Returns null, if the object cannot be pushed to the stack.
   */
  public Object push(Object o) {
    // TODO
    if(size == stack.length) return null;
    stack[size++] = o;
    return o;
  }

  /**
   * Pops the first item from the stack.
   *
   * @return the object, iff the object has been popped from stack successfully. Null, if the stack is empty.
   */
  public Object pop() {
    // TODO
    if(size == 0) return null;
    Object o = stack[size-1];
    size--;
    return o;
  }

  /**
   * Check the item on top of the stack, without removing it.
   *
   * @return the top object, iff the stack has an item. Null, if the stack is empty.
   */
  public Object peek() {
    // TODO
    if(size == 0) return null;
    return stack[size-1];
  }
}
```
