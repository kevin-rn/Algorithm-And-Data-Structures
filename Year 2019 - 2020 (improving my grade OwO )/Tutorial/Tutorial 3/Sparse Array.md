A popular activity for scouts is to sell cookies door to door. 
These cookies are baked by the scouts and then sold to neighbours to raise funds to support their activities. 
Your scouting group ADS (Algorithms and Data Scouts) is planning to organize this activity, 
however, you have been told by other people that some of your neighbours are rather grumpy and mean, 
they will never buy any single cookie from you and will only yell at you. 
To prevent the young fledglings from getting disappointed, you have asked the Mayor to give you all the information of the inhabitants in your street. 
This information can be found in the class Street. It contains an array storing information about the inhabitants of this street, 
the index of the array is the house number and the element stored at that position is the name of the inhabitant.

Your task is to first go over this array and remove all inhabitants that have been marked as mean. 
However, as your street is named Grumpystreet, most of its inhabitants are grumpy. 
So, when you decided to print out the information of the friendly people in this street, 
you noticed that you were printing a lot of removed entries in the array. 
To fix this, you have decided to use another data structure, namely a list of Houses, 
this class is used to store tuples of the house number combined with the name of the owner of that house, 
this means that all the removed entries will not be stored anymore.

### Library
```java
class Street {

  private String[] inhabitants;

  public Street(int n) {
    this.inhabitants = new String[n];
  }

  public Street(List<String> inhabitants) {
    this.inhabitants = new String[inhabitants.size()];
    for (int i = 0; i < inhabitants.size(); i++) {
      this.inhabitants[i] = inhabitants.get(i);
    }
  }

  public String getNeighbour(int i) throws IllegalArgumentException {
    if (i < 0 || i >= inhabitants.length) {
      throw new IllegalArgumentException("No neighbour at that index.");
    }
    return this.inhabitants[i];
  }

  public void removeNeighbour(int i) throws IllegalArgumentException {
    if (i < 0 || i >= inhabitants.length) {
      throw new IllegalArgumentException("No neighbour at that index.");
    }
    this.inhabitants[i] = null;
  }

  public void addNeighbour(int i, String neighbour) throws IllegalArgumentException {
    if (i < 0 || i >= inhabitants.length) {
      throw new IllegalArgumentException("No neighbour at that index.");
    }
    this.inhabitants[i] = neighbour;
  }

  public int size() {
    return this.inhabitants.length;
  }

  public String toString() {
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < this.inhabitants.length; i++) {
      sb.append(i);
      sb.append(": ");
      sb.append(this.inhabitants[i]);
      sb.append("\n");
    }
    return sb.toString();
  }
}

class House {

  private int houseNumber;

  private String owner;

  public House(int houseNumber, String owner) {
    this.houseNumber = houseNumber;
    this.owner = owner;
  }

  public String toString() {
    return this.houseNumber + ": " + owner;
  }

  @Override
  public boolean equals(Object o) {
    if (this == o)
      return true;
    if (o == null || this.getClass() != o.getClass())
      return false;
    House house = (House) o;
    return houseNumber == house.houseNumber && Objects.equals(owner, house.owner);
  }
}

```

### Solution
```java
import java.util.*;

class CookieList {

  Street street;

  public CookieList(Street street) {
    this.street = street;
  }

  /**
   * Prunes the street, to remove all mean people.
   * @param meanPeople - the list of mean people that will need to be removed from the array of street
   */
  public void pruneStreet(List<String> meanPeople) {
    for(int i =0; i < street.size(); i++) {
        if(meanPeople.contains(street.getNeighbour(i))) street.removeNeighbour(i);
    }
  }

  /**
   * Turns the sparse array containing all nice people in the street into a list,
   * where each element is a House object that stores the house number and name of the inhabitant.
   * @return a list of houses with all the nice people
   */
  public List<House> listAllFriendlyHouses() {
    ArrayList<House> houses = new ArrayList<>();
    for(int i =0; i<street.size(); i++) {
      if(street.getNeighbour(i) != null) houses.add(new House(i, street.getNeighbour(i)));
    }
    return houses;
  }
}


```
