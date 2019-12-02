Implement the method checkPalindrome, which takes a sequence of characters implemented by a singly linked list (SLList) and checks whether the sequence is a palindrome using a stack (LibraryStack).

Each node of the singly linked list stores a character of the sequence as an element.

For example, if the singly linked list stores the sequence apple, the list will have 5 nodes (one per character): the head node storing character a, the next node containing character p, and so on.

A palindrome is a sequence that reads the same backwards as forwards. For example these words are palindromes:

    level
    anna
    mom
    radar
    madam

You can assume that all characters are lowercase.

We provide implementations of classes SLList (singly linked list) and LibraryStack (stack) as visible Library code.

Important: Your implementation will need to satisfy the following requirements:

    You are not allowed to use a String object.
    Your implementation needs to make use of the library stack that we provided.
    You are not allowed to use any data structures other than the library stack that we provided.
    The complexity of your implementation needs to be O(n) where n is the size of the singly linked list.

```java
class Solution {
  /**
   * Checks for a String represented as a SLList whether this String is a palindrome.
   * This is done by using a stack.
   *
   * An empty String or null should return true.
   *
   * @param list
   *     SLList used to represent a String
   * @return true if the String represented as a SLList is a palindrome, otherwise false
   */
  public static boolean checkPalindrome(SLList list) {
    if(list == null || list.size() == 0) return true;
    LibraryStack<Character> stack = new LibraryStack<>();
    LibraryStack<Character> stack2 = new LibraryStack<>();
    LibraryStack<Character> reverse = new LibraryStack<>();
    int size = list.size();
    
    boolean uneven = false;
    if(size % 2 != 0) {
      size = (size-1)/2;
      uneven = true;
    }
    else size = size/2;
    
    for(int i = 0; i < size; i++) stack.push(list.removeFirst());
    if(uneven) list.removeFirst();
    for(int i = 0; i < size; i++) reverse.push(list.removeFirst());
    while(!reverse.isEmpty()) stack2.push(reverse.pop());
    
    while(!stack.isEmpty()) {
      if(stack.pop() != stack2.pop()) return false;
    }
    
    return true;
  }
}


```
