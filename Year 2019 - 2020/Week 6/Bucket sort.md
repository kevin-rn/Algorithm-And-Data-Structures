### Bucket Sort (2/6)
In this assignment, you will implement bucket sort.

First, implement the method fillBuckets() which sorts the elements from an array into an array of buckets. For simplicity, the input array only contains keys but no associated values. The output is an array of buckets, where each bucket is represented as a Queue.

First determine the minimum and maximum values of array and store them in variables vmin and vmax. You should return an array of buckets of size vmax-vmin+1. Each bucket should be represented as a Queue of values, where bucket[i] stores values v = vmin + i.

Do not implement the Queue interface yourself. You can use any data structure from the Java libraries, which implement the Queue interface.

After filling the buckets, implement the method readBuckets(), which turns the buckets that you have created in fillBuckets() into a sorted array.

```java
import java.util.*;

class Solution {
  @SuppressWarnings("unchecked")
  public static Queue<Integer>[] fillBuckets(int[] array) {
    if(array == null || array.length == 0) return new Queue[0];
    int vmin = 0;
    int vmax = 0;
    
    for(int i=1; i<array.length; i++) {
      if(array[vmin] > array[i]) vmin = i;
      if(array[vmax] < array[i]) vmax = i;
    }
    
    Queue<Integer>[] buckets = new Queue[array[vmax] - array[vmin] + 1];
    
    for(int i = 0; i < array.length; i++) {
      int idx = array[i]-array[vmin];
      if(buckets[idx] == null) buckets[idx] = new PriorityQueue<Integer>();
      buckets[idx].add(array[i]);
    }
     
    return buckets;
  }

  public static int[] readBuckets(Queue<Integer>[] buckets) {
    int size =0;
    for(int i=0; i<buckets.length;i++) {
      if(buckets[i] != null) size += buckets[i].size();
    }

    int[] array = new int[size];

     for(int i = 0, j =0; i < buckets.length; i++){
      if(buckets[i] != null){
        array[j++] = buckets[i].poll();
      }
    }
    return array;
  }
}
```
