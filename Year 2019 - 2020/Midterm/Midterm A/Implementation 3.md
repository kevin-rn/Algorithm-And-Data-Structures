Implement a sorting algorithm with a priority queue. You will need to implement the following methods:

  pqSort
  upHeap

The method pqSort takes as input a list of integers and returns a sorted list in decreasing order, your implementation should use the priority queue to sort.

The method upHeap takes as input an integer representing the index of the node that has been added to the heap.

We provide implementation of the class LibraryPQ (priority queue). 
The method upHeap is abstract, the class SolutionPQ extends LibraryPQ and you will need to implement the method upHeap there.

### Library
```java
abstract class LibraryPQ {
  private List<Integer> heap;

  public LibraryPQ() {
    heap = new ArrayList<>();
  }

  /**
   * Swaps two elements in an array.
   *
   * @param i
   *     Position of element to swap in a.
   * @param j
   *     Position of element to swap in a.
   */
  public void swap(int i, int j) {
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
   * @param i
   *     index of the node
   */
  public abstract void upHeap(int i);

  /**
   * Inserts the specified element into this priority queue.
   *
   * @param i
   *     element to add
   */
  public void insert(int i) {
    heap.add(i);
    upHeap(heap.size() - 1);
  }

  /**
   * Retrieves and removes the first element of this priority queue.
   *
   * @return the first element of the queue
   */
  public int removeMax() {
    int i = heap.get(0);
    swap(0, heap.size() - 1);
    heap.remove(heap.size() - 1);
    downHeap(0, heap.size() - 1);
    return i;
  }

  /**
   * Returns the element at the i-th position in the heap.
   *
   * @param i
   *     the index of the position
   * @return element with index i
   */
  public int getInHeap(int i) {
    return heap.get(i);
  }

  /**
   * Checks if another heap represented as a list is equal to this heap.
   *
   * @param l
   *     list representing a heap
   * @return true iff the two lists are equal
   */
  public boolean heapEquals(List<Integer> l) {
    return this.heap.equals(l);
  }
}
```

### Solution
```java
import java.util.*;

class Solution {
  /**
   * Takes a list and returns a new list sorted in descending order.
   * This is done by using the priority queue `queue`.
   *
   * Return null if list is null.
   *
   * @param list
   *     the array that needs to be sorted.
   */
  public static List<Integer> pqSort(List<Integer> list) {
    LibraryPQ queue = new SolutionPQ();
    if (list == null || list.size() <= 1) return list;
    for (Integer x : list) queue.insert(x);
    for (int i = 0; i < list.size(); i++) list.set(i, queue.removeMax());
    return list;

  }
}

class SolutionPQ extends LibraryPQ {
  /**
   * Restores the heap property in a heap represented as an arraylist.
   * The method compares the node to its parent and swaps if necessary.
   *
   * @param i
   *     index of the node
   */
  @Override
  public void upHeap(int i) {
    if (i == 0) return;
      int parent;
      // if index is even, i is right child:
      if (i % 2 == 0) parent = (i - 2) / 2;
      else parent = (i - 1) / 2;
     
      if (this.getInHeap(i) > this.getInHeap(parent)) this.swap(i, parent);
      this.upHeap(parent);
  }
}

```
