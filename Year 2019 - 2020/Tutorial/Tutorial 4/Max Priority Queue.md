In this exercise you are given the implementation of a heap-based priority queue that returns the minimum element in the priority queue. 
Your task is to change this to a priority queue that returns the maximum value first.

### Template
```java
import java.util.*;

class SolutionPQ {

  private List<Integer> heap;

  public SolutionPQ() {
    heap = new ArrayList<>();
  }

  /**
   * Swaps two elements in the list.
   *
   * @param i
   *     Position of element to swap in a.
   * @param j
   *     Position of element to swap in a.
   */
  private void swap(int i, int j) {
    int t = heap.get(i);
    heap.set(i, heap.get(j));
    heap.set(j, t);
  }

  /**
   * Restores the heap property in a heap represented as an arraylist.
   * When the heap property is invalid at root,
   * the method fixes the heap first locally before fixing the affected subtree.
   *
   * @param root
   *     Index of the root of the heap, which might be a subtree of the overall heap.
   * @param range
   *     Index of the last element in the heap, array elements with an index > range are not part of the heap.
   */
  public void downHeap(int root, int range) {

    // index of left and right children
    int left = 2 * root + 1;
    int right = 2 * root + 2;

    int smallest;

    if (left <= range && heap.get(left) < heap.get(root))
      smallest = left;
    else
      smallest = root;

    if (right <= range && heap.get(right) < heap.get(smallest))
      smallest = right;

    // heap property invalid at root
    if (smallest != root) {
      swap(root, smallest);
      downHeap(smallest, range);
    }
  }

  /**
   * Restores the heap property in a heap represented as an arraylist.
   * The method compares the node to its parent and swaps if necessary.
   *
   * @param i index of the node
   */
  public void upHeap(int i) {
    while (i >= 1) {
      int j = (i - 1) / 2;
      if (heap.get(j) <= heap.get(i))
        break;
      swap(j,i);
      i = j;
    }
  }

  /**
   * Inserts the specified element into this priority queue.
   *
   * @param i
   *     element to add
   */
  public void add(int i) {
    heap.add(i);
    upHeap(heap.size() - 1);
  }

  /**
   * Retrieves and removes the first element of this priority queue.
   *
   * @return the first element of the queue
   */
  public int poll() {
    int i = heap.get(0);
    swap(0, heap.size() - 1);
    heap.remove(heap.size() - 1);
    downHeap(0, heap.size() - 1);
    return i;
  }

  /**
   * @return the current number of elements in the heap
   */
  public int size() {
    return this.heap.size();
  }
}


```

### Solution (change direction of some comparisons)
```java
import java.util.*;

class SolutionPQ {

  private List<Integer> heap;

  public SolutionPQ() {
    heap = new ArrayList<>();
  }

  /**
   * Swaps two elements in the list.
   *
   * @param i
   *     Position of element to swap in a.
   * @param j
   *     Position of element to swap in a.
   */
  private void swap(int i, int j) {
    int t = heap.get(i);
    heap.set(i, heap.get(j));
    heap.set(j, t);
  }

  /**
   * Restores the heap property in a heap represented as an arraylist.
   * When the heap property is invalid at root,
   * the method fixes the heap first locally before fixing the affected subtree.
   *
   * @param root
   *     Index of the root of the heap, which might be a subtree of the overall heap.
   * @param range
   *     Index of the last element in the heap, array elements with an index > range are not part of the heap.
   */
  public void downHeap(int root, int range) {
    // index of left and right children
    int left = 2 * root + 1;
    int right = 2 * root + 2;
    int largest;
    if (left <= range && heap.get(left) > heap.get(root))
      largest = left;
    else
      largest = root;
    if (right <= range && heap.get(right) > heap.get(largest))
      largest = right;
    // heap property invalid at root
    if (largest != root) {
      swap(root, largest);
      downHeap(largest, range);
    }
  }

  /**
   * Restores the heap property in a heap represented as an arraylist.
   * The method compares the node to its parent and swaps if necessary.
   *
   * @param i index of the node
   */
  public void upHeap(int i) {
    while (i >= 1) {
      int j = (i - 1) / 2;
      if (heap.get(j) >= heap.get(i))
        break;
      swap(j, i);
      i = j;
    }
  }

  /**
   * Inserts the specified element into this priority queue.
   *
   * @param i
   *     element to add
   */
  public void add(int i) {
    heap.add(i);
    upHeap(heap.size() - 1);
  }

  /**
   * Retrieves and removes the first element of this priority queue.
   *
   * @return the first element of the queue
   */
  public int poll() {
    int i = heap.get(0);
    swap(0, heap.size() - 1);
    heap.remove(heap.size() - 1);
    downHeap(0, heap.size() - 1);
    return i;
  }

  /**
   * @return the current number of elements in the heap
   */
  public int size() {
    return this.heap.size();
  }
}

```
