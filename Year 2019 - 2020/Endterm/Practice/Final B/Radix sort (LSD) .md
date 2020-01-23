In this assignment, you are expected to implement the LSD (least-significant-digit-first) radix sort algorithm to sort a sequence of Dutch mobile phone numbers in non-decreasing order.

For example, if the content of the input array is [0687654321, 0612301345, 0612300123, 0612345678], the content of the output array should be [0612300123, 0612301345, 0612345678, 0687654321].

You may assume that every String in the input array starts with 06 and is followed by eight digits.

Your algorithm needs to run in O(n)
time, where n

is the number of items to sort.

If null is passed as argument, radixSortLSD should throw a NullPointerException.

### Template:
```java
import java.util.*;

class Solution {
  /**
   * Sorts a list of Dutch mobile phone numbers using LSD radix sort.
   *
   * @param phoneNumbers
   *     The list of phone numbers to sort.
   * @return The sorted list of phone numbers.
   * @throws NullPointerException
   *     If `phoneNumbers` equals `null`.
   */
  static List<String> radixSortLSD(List<String> phoneNumbers) {
    // TODO
  }
}

```

### Test:
```java
import org.junit.*;

import java.util.ArrayList;
import java.util.*;

import static java.util.Arrays.*;
import static org.junit.Assert.*;

public class UTest {
  @Test(timeout = 100)
  public void testEmpty() {
    assertEquals(new ArrayList<>(), Solution.radixSortLSD(new ArrayList<>()));
  }

  @Test(timeout = 100)
  public void testReversed() {
    List<String> data = asList("0644444444", "0633333333", "0622222222", "0611111111");
    List<String> data2 = asList("0611111111", "0622222222", "0633333333", "0644444444");
    assertEquals(data2, Solution.radixSortLSD(data));
  }
}


```

_________________________________________________________________________________________________________


### Solution:
```java
import java.util.*;

class Solution {
  /**
   * Sorts a list of Dutch mobile phone numbers using LSD radix sort.
   *
   * @param phoneNumbers
   *     The list of phone numbers to sort.
   * @return The sorted list of phone numbers.
   * @throws NullPointerException
   *     If `phoneNumbers` equals `null`.
   */
  static List<String> radixSortLSD(List<String> phoneNumbers) {
    if(phoneNumbers == null) throw new NullPointerException();
    return sort(phoneNumbers, 9);
  }
  
  @SuppressWarnings("unchecked")
  static List<String> sort(List<String> phone, int idx) {
    List<String> list = new LinkedList<>();
    //Base case
    if(idx == 1) return phone;
    
    //Create different 'buckets' for holding specific numbers e.g. 1, 2, 3...9
    LinkedList<String>[] numbers = new LinkedList[10];
    for(int i =0; i<10; i++) numbers[i] = new LinkedList<>();
    
    //Add them in the right list
    for(String p : phone) numbers[p.charAt(idx) - '0'].add(p);
    
    //Get them out of the 'buckets' and put them in the result
    //Note: This is still O(n) as the outer loop is a small value which we can discard -> O(10N) -> O(n) 
    for(int i = 0; i<10; i++) {
      for(String p:numbers[i]) list.add(p);
    }
    
    //Go to next number
    return sort(list, idx-1);
  }
}


```
