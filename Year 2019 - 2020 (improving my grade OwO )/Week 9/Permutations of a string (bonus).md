### Permutations of a string (bonus)

Implement a method permuteString, which calculates all permutations of a string s.  
Implement a helper method findPermutations, which uses backtracking to find all possible permutations.  
You can instantiate a set of strings using new TreeSet<String>().

Example: For s = "abc", possible permutations abc, acb, bac, bca, cab, and cba.  

### Template:
```java
import java.util.*;

class Solution {
  static Set<String> permuteString(String s) {
    Set<String> result = new TreeSet<>();
    // TODO
    return result;
  }
}
```


### Test:
```java
import org.junit.*;

import java.util.*;

import static org.junit.Assert.*;

public class UTest {
  @Test
  public void test1Letter() {
    Set<String> expected = new TreeSet<>();
    expected.add("a");
    assertEquals(expected, Solution.permuteString("a"));
  }

  @Test
  public void test2Letters() {
    Set<String> expected = new TreeSet<>();
    Collections.addAll(expected, "ab", "ba");
    assertEquals(expected, Solution.permuteString("ab"));
  }

  @Test
  public void test3Letters() {
    Set<String> expected = new TreeSet<>();
    Collections.addAll(expected, "abc", "acb", "bac", "bca", "cab", "cba");
    assertEquals(expected, Solution.permuteString("abc"));
  }

  @Test
  public void test4Letters() {
    Set<String> expected = new TreeSet<>();
    Collections.addAll(expected, "abcd", "abdc", "acbd", "acdb", "adbc", "adcb", "bacd", "badc", "bcad", "bcda", "bdac", "bdca", "cabd", "cadb", "cbad", "cbda", "cdab", "cdba", "dabc", "dacb", "dbac", "dbca", "dcab", "dcba");
    assertEquals(expected, Solution.permuteString("abcd"));
  }
}
```

________________________________________________________________________________________________________________________________


### Solution:
```java
import java.util.*;

class Solution {
  public static Set<String> result;
  
  static Set<String> permuteString(String s) {
    result = new TreeSet<>();
    Permutation(s, "");
    return result;
  }
  
   static void Permutation(String s, String ans) { 
        if (s.length() == 0) { 
            result.add(ans); 
            return; 
        } 
        for (int i = 0; i < s.length(); i++) { 
            char ch = s.charAt(i); 
            String ros = s.substring(0, i) + s.substring(i + 1); 
            Permutation(ros, ans + ch); 
        } 
    } 
}
```
