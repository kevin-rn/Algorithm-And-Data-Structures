In this exercise we will revise the array list implementation given in Section 7.2.1 of the book [^1]. Remember that the array list is implemented with an underlying array, when the capacity of the array has been reached, we can increase the capacity by simply creating a new array with a larger capacity and transferring all elements from the original array to the new one.

However, in the original implementation of the book the capacity of this array would never shrink after increasing. Your task is to improve this, by also halving the capacity of the array whenever the actual number of elements in the array goes below N/4, where N is the capacity of the array.

For this purpose the original implementation of the array list as described in the book is given to you, you will need to adapt the code to take care of the shrinking process. Some tests have been included to further show you the intended behaviour of the array list.

[^1]: Michael T. Goodrich, Roberto Tamassia, Michael H. Goldwasser, Data Structures and Algorithms in Java

```java

class ADSArrayList<T> {

  // Default initial capacity used for the array list
  public static final int CAPACITY = 16;

  // Underlying array to store the elements
  private T[] data;

  // Amount of elements in the array list
  private int size;

  /**
   * Constructor to create an array list with default initial capacity.
   */
  public ADSArrayList() {
    this(CAPACITY);
  }

  /**
   * Constructor to create an array list with a specific initial capacity
   * @param capacity - initial capacity for this array list
   */
  public ADSArrayList(int capacity) {
    this.data = (T[]) new Object[capacity];
    this.size = 0;
  }

  /**
   * @return the amount of elements in the array list
   */
  public int size() {
    return this.size;
  }

  /**
   * @return the current capacity of the array list
   */
  public int getCapacity() {
    return this.data.length;
  }

  /**
   * @return true if the array list is empty, else false
   */
  public boolean isEmpty() {
    return this.size == 0;
  }

  /**
   * @param i - index of the lookup
   * @return the element at the specified index
   * @throws IndexOutOfBoundsException if there is no element at that index
   */
  public T get(int i) throws IndexOutOfBoundsException {
    if (i < 0 || i >= this.size) {
      throw new IndexOutOfBoundsException("Illegal index: " + i);
    }
    return this.data[i];
  }

  /**
   * Changes the element stored at a certain position.
   * @param i - index to store the element
   * @param e - the new element
   * @return the previous element stored at that position
   * @throws IndexOutOfBoundsException if there is no element at that index
   */
  public T set(int i, T e) throws IndexOutOfBoundsException {
    if (i < 0 || i >= this.size) {
      throw new IndexOutOfBoundsException("Illegal index: " + i);
    }
    T temp = this.data[i];
    this.data[i] = e;
    return temp;
  }

  /**
   * Adds a new element at the end of the array list
   * @param e - new element to be added
   */
  public void add(T e) {
    add(size, e);
  }

  /**
   * Adds an element at a specific index, shifting all other elements after it
   * @param i - index to store the element
   * @param e - the new element
   * @throws IndexOutOfBoundsException if the specified index is out of bounds (i.e. the specified index is not a possible position in the array or leaves a gap between the new element and existing elements)
   */
  public void add(int i, T e) throws IndexOutOfBoundsException {
    if (i < 0 || i > this.size) {
      throw new IndexOutOfBoundsException("Illegal index: " + i);
    }
    if (this.size == this.data.length) {
      resize(2 * this.data.length);
    }
    for (int k = this.size - 1; k >= i; k--) {
      this.data[k + 1] = this.data[k];
    }
    this.data[i] = e;
    this.size++;
  }

  /**
   * Removes an element at a specific index, shifting all other elements after it
   * @param i - index to remove the element
   * @return the element at the specified index
   * @throws IndexOutOfBoundsException if there is no index at that index
   */
  public T remove(int i) throws IndexOutOfBoundsException {
    if (i < 0 || i >= this.size) {
      throw new IndexOutOfBoundsException("Illegal index: " + i);
    }
    T temp = this.data[i];
    for (int k = i; k < this.size - 1; k++) {
      this.data[k] = this.data[k + 1];
    }
    this.data[size - 1] = null;
    this.size--;
    if(getCapacity()/4 > size()) resize(getCapacity()/2);
    return temp;
  }

  /**
   * Resizes the array to the specified capacity, moving all elements from the old array to the new one
   * @param capacity - new capacity for the array
   */
  private void resize(int capacity) {
    T[] res = (T[]) new Object[capacity];
    for (int k = 0; k < this.size; k++) {
      res[k] = this.data[k];
    }
    this.data = res;
  }
}


```
