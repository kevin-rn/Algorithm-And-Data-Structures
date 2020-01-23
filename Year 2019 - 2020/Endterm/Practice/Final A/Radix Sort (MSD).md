In this assignment, you are expected to implement the MSD (most-significant-digit-first) radix sort algorithm to sort a sequence of words in non-decreasing alphabetic order.

For example, if the content of the input array is [pig, cat, parrot, monkey], the content of the output array should be [cat, monkey, parrot, pig].

You may assume that every String in the input array only contains of the lowercase letters (meaning the 26 letters a through z in the English alphabet).

Your algorithm needs to run in O(n⋅l)
time, where n is the number of items to sort and l

is the average length of a word.

If null is passed as argument, radixSortMSD should throw a NullPointerException.

### Template:
```java
import java.util.*;

class Solution {
  /**
   * Sorts a list of words using MSD radix sort.
   *
   * @param words
   *     The list of words to sort.
   * @return The sorted list of words.
   * @throws NullPointerException
   *     If `words` equals `null`.
   */
  static List<String> radixSortMSD(List<String> words) {
    // TODO
  }
}

```

### Test
```java
import org.junit.*;

import java.util.ArrayList;
import java.util.*;

import static java.util.Arrays.*;
import static org.junit.Assert.*;

public class UTest {
  @Test(timeout = 100)
  public void testEmpty() {
    assertEquals(new ArrayList<>(), Solution.radixSortMSD(new ArrayList<>()));
  }

  @Test(timeout = 100)
  public void testReversed() {
    List<String> data = asList("donut", "cherry", "banana", "apple");
    List<String> data2 = asList("apple", "banana", "cherry", "donut");
    assertEquals(data2, Solution.radixSortMSD(data));
  }
}


```

___________________________________________________________________________________________________

### Solution:
```java
import java.util.*;

class Solution {
  /**
   * Sorts a list of words using MSD radix sort.
   *
   * @param words
   *     The list of words to sort.
   * @return The sorted list of words.
   * @throws NullPointerException
   *     If `words` equals `null`.
   */
  static List<String> radixSortMSD(List<String> words) {
    if(words == null) throw new NullPointerException();
    return sort(words, 0);
  }
  
  @SuppressWarnings("unchecked")
  static List<String> sort(List<String> words, int idx) {
    List<String>[] buckets = new LinkedList[26];
    List<String> result = new LinkedList<>();
    for(int i =0; i<26; i++) buckets[i] = new LinkedList<>();
    
    //if words are shorter than current index add them to result else add them to te buckets
    for(String s:words) {
      if(s.length()-1 < idx) result.add(s);
      else buckets[s.charAt(idx) - (int)'a'].add(s);
    }
    
    for(int i =0; i<26; i++) {
      if(buckets[i].size() > 0) buckets[i] = sort(buckets[i], idx+1);
    }
    
    for(int i = 0; i<26; i++) {
      for(String s : buckets[i]) result.add(s);
    }
    
    return result;
  }
}


```
