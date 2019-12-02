You are playing card games with your friend Bob during the shared labs, however every single time that you try to shuffle the cards, 
Bob will stop you and rant about shuffling the deck properly. 
His idea is that each time you shuffle you will need to split the deck of cards into two equally large decks and then merge 
these two back together by alternating between a card from one half and another card from the other half. 
This way the deck will be shuffled “properly”.

While, you do not mind having to shuffle the deck in this particular fashion, you do find it quite time consuming. 
So, you suggested writing an algorithm to do the shuffling process as described by Bob.

Note that the deck will have 2n elements where n <= 26. This exercise can be found in chapter 7 of the book.

### Library
```java
class Card {

  public Num number;

  public Suit suit;

  public Card(Num number, Suit suit) {
    this.number = number;
    this.suit = suit;
  }

  public Card(int number, int suit) {
    this.number = Num.get(number);
    this.suit = Suit.get(suit);
  }

  public String toString() {
    return this.number.toString().toLowerCase() + " of " + this.suit.toString().toLowerCase();
  }
  
  public boolean equals(Object other) {
    if (other instanceof Card) {
      Card that = (Card) other;
      return this.number.equals(that.number) && this.suit.equals(that.suit);
    }
    return false;
  }
}

enum Suit {

  DIAMONDS(0), CLUBS(1), HEARTS(2), SPADES(3);

  private static final Map<Integer, Suit> lookup = new HashMap<>();

  static {
    for (Suit s : EnumSet.allOf(Suit.class)) {
      lookup.put(s.getCode(), s);
    }
  }

  private int code;

  Suit(int code) {
    this.code = code;
  }

  public int getCode() {
    return this.code;
  }

  public static Suit get(int code) {
    return lookup.get(code);
  }
}

enum Num {

  ACE(1),
  TWO(2),
  THREE(3),
  FOUR(4),
  FIVE(5),
  SIX(6),
  SEVEN(7),
  EIGHT(8),
  NINE(9),
  TEN(10),
  JACK(11),
  QUEEN(12),
  KING(13);

  private static final Map<Integer, Num> lookup = new HashMap<>();

  static {
    for (Num n : EnumSet.allOf(Num.class)) {
      lookup.put(n.getCode(), n);
    }
  }

  private int code;

  Num(int code) {
    this.code = code;
  }

  public int getCode() {
    return this.code;
  }

  public static Num get(int code) {
    return lookup.get(code);
  }
}

```

### Solution
```java
import java.util.*;

class Solution {
  /**
   * Shuffles a deck of cards. This is done by splitting the existing deck into two halves, L1 and L2.
   * The two halves will be merged back together by taking alternating elements from L1 and L2.
   * Where the order is as follows:
   * first element of L1, first element of L2, second element of L1, second element of L2, and so forth.
   *
   * @param deck
   * @return
   */
  public static List<Card> cardShuffle(List<Card> deck) {
    List<Card> h1 = new ArrayList<>(deck.subList(0, deck.size()/2)), h2 = new ArrayList<>(deck.subList(deck.size()/2, deck.size())), result = new ArrayList<>();
    for(int i =0; i<deck.size()/2; i++) {
      result.add(h1.get(i));
      result.add(h2.get(i));
    }
    return result;
  }
}
```
