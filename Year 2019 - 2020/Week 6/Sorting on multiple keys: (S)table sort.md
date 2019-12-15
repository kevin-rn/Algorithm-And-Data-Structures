### (S)Table sort (3/6)
In this assignment, you will implement a stable sorting algorithm that can be used to sort tables of Strings.

As input, you will receive a two-dimensional array (a table) of Strings and the index of the “column” you should sort. You should sort the rows by the values in the indicated column.

You can see the first index as a row index, and the second index as a column index. For example, the following Java array and table correspond with each other:

String[][] table = {
  {"a", "b"},
  {"c", "d"}
};

    0   1
  +---+---+
0 | a | b |
  +---+---+
1 | c | d |
  +---+---+

To continue on this example, table[0][1] will yield the value "b", since it’s the item in row 0 and column 1.

You are allowed to implement any stable sorting algorithm with a worst-case time complexity of O(n2).
(Remember that this includes algorithms with a complexity of O(nlogn).)

IMPORTANT: You are not allowed to use any sorting algorithm from the Java library, for example Arrays.sort. If you do use a Java library function to sort the array, your grade will be overridden to 1.

```java
class Solution {
public static void stableSort(String[][] table, int column) {
        for (int i = 1; i < table.length; i++) {
            for(int j = i ; j > 0 ; j--){
                if(table[j][column].compareTo(table[j-1][column]) < 0){
                    String[] temp = table[j];
                    table[j] = table[j-1];
                    table[j-1] = temp;
                }
            }
        }
    }
}
```



