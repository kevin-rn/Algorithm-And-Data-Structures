### Knapsack

Implement a solution to the knapsack problem, preferably using backtracking.  
You will get a list of items, each with a specific weight and value.  
Given a certain budget, you must return a list of items of which the combined weight does not exceed this budget, and their combined value is maximized.
The Item class has a getWeight() and a getValue() method, to get its weight and value, respectively.  
There are ways of finishing this assignment without backtracking, but the TAs will only provide help if you do use backtracking. 
Your grade does not depend on whether you use backtracking or not.  

### Template:
```java
import java.util.*;

class Solution {
  /**
   * Calculates the most optimal set of items that should be put in the knapsack using backtracking.
   *
   * @param items
   *     The items that you can choose from.
   * @param budget
   *     The maximum weight that the knapsack can carry.
   * @return The optimal set of items that should be put in the knapsack.
   */
  public static Set<Item> knapsack(Set<Item> items, int budget) {
    // TODO
  }
}

```
  
   
   
### Solution:   
```java   
import java.util.*;

class Solution {
  /**
   * Calculates the most optimal set of items that should be put in the knapsack using backtracking.
   *
   * @param items
   *     The items that you can choose from.
   * @param budget
   *     The maximum weight that the knapsack can carry.
   * @return The optimal set of items that should be put in the knapsack.
   */
  public static Set<Item> knapsack(Set<Item> items, int budget) {
    int n = items.size(), a = 0;
    int[] val = new int[n], wt = new int[n];
    ArrayList<Item> set = new ArrayList<>();
    for(Item i : items) {
      set.add(i);
      val[a] = i.getValue();
      wt[a++] = i.getWeight();
    }
    boolean[] visited = new boolean[n];
    knapSack(budget, wt, val, n, visited);
    Set<Item> result = new HashSet<>();
    for(int i = 0; i < n; i++) {
      if(visited[i]) result.add(set.get(i));
    }
    return result;
    
  }
  
  //knapsack method for checking which items fit in the budget
  static int knapSack(int budget, int[] wt, int[] val, int n, boolean[] visited) {
      if (n == 0 || budget == 0) return 0;
      if (wt[n-1] > budget) return knapSack(budget, wt, val, n-1,visited);
      else {
        boolean v1[]=new boolean[visited.length];
        System.arraycopy(visited, 0, v1, 0, v1.length);
        boolean v2[]=new boolean[visited.length];
        System.arraycopy(visited, 0, v2, 0, v2.length);
        v1[n-1]= true;
        int ans1 = val[n-1] + knapSack(budget-wt[n-1], wt, val, n-1,v1);
        int ans2 = knapSack(budget, wt, val, n-1,v2);
        if(ans1>ans2){
            System.arraycopy(v1, 0, visited, 0, v1.length);
            return ans1;
        } else{
            System.arraycopy(v2, 0, visited, 0, v2.length);
            return ans2;
        }
    }            
  }
  
  //compares two ints
  static int max(int a, int b) { return (a > b)? a : b; } 
}
```
