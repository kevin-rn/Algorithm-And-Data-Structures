Implement method findMiddleInLastLayer, which returns the middle node in the last level of a heap with n elements implemented using a linked binary tree.

The time complexity of the method should be O(h), where h is the height of the tree.

For the example heap in the figure below, the middle node in the last level corresponds to the node highlighted in yellow.

![](figure-heap-middlenode-lastlevel.png)

Remember that the number of nodes in the last level can be calculated using the total number of nodes n in the heap, since a heap is a complete binary tree.

In addition, you can obtain the path from the root to any node in the last level by taking the rightmost h bits in the binary representation of the index of such node within the last level.  
Each bit indicates which child to follow at each level: 0 for left and 1 for right.

For the example heap in the figure above:
  The height is 3.
  The middle position has index 2 which translates into the following 32-bit representation: 00000000 00000000 00000000 00000010
  Taking the h rightmost bits in this binary representation results in 010, indicating that we can directly follow the path 
  left -> right -> left from the root in order to find the middle node in the last level.

If the index is stored as an integer variable in Java (int index;), you can use a bit mask to sequentially extract the bits of the path as follows:

  Create bit mask to extract the first bit: int mask = 1 << (h-1); (shift 0..00 0..00 0..00 0..001 left h-1 times, resulting in 0..00 0..00 0..00 0..100 for the example above)
  Update mask for next level: mask >> 1 (shift current mask once to the right: if the current mask is 0..00 0..00 0..00 0..100, this will result in 0..00 0..00 0..00 0..010)
  Test the bit using the current mask to decide left or right at the current level: index & mask (bitwise “and” operation that evaluates to 0 if the given bit is 0, or non-zero integer if the given bit is 1)

We provide an implementation of class Heap (and its inner class Node) in the visible Library code.

An object of type Heap stores a reference to the root Node of the heap and also the total number of Nodes in the heap, which can be obtained by calling methods getRoot and size, respectively.

Each Node in the Heap has a reference to its left child Node and a reference to its right child Node (each reference can be null if the child does not exist). These are not directly available via the Node, they can be accessed using methods in the Heap class.

Note that if you want to access the Node class, you need to write Heap.Node (you can find examples of this in the visible Library code).

IMPORTANT: If the complexity of your solution is not O(h), you will get 0 points for this assignment.

```java
class Solution {
  /**
   * @param heap
   *     the Heap to check, can be null. If not null, this heap will always contain at least one Node.
   * @return the Node corresponding to the middle element in the last layer of the Heap, or null if the Heap is null.
   * In case the last layer contains an even number of elements, returns the element just left of the middle (see test).
   */
	  public static Heap.Node findMiddleInLastLayer(Heap heap) {
		  if (heap == null || heap.size() == 0) return null;
		  if (heap.size() == 1) return heap.getRoot();
		  int size = heap.size();
		  int height = (int) Math.floor(Math.log10(size) / Math.log10(2));
		  int max_nodes = (int)Math.pow(2, height+1) - 1;
		  int max_nodes_last_level = (int)Math.pow(2, height);
		  int nodes_last_level = max_nodes_last_level - (max_nodes - size);
		  
		  int middle;
		  if (nodes_last_level % 2 == 0) {
			  middle  = nodes_last_level / 2 - 1;
		  } else {
			  middle = nodes_last_level / 2;
		  }
		  
		  int mask = 1 << (height - 1);
		  
		  int count = 0;
		  Heap.Node res = heap.getRoot();
		  
		  while (count < height) {
			  if ((middle & mask) == 0) {
				  res = heap.getLeft(res);

			  } else {
				  res = heap.getRight(res);
			  }
			  mask = mask >> 1;
		  	  count++;
		  }
		  
		  return res;
	  }
	}
```

