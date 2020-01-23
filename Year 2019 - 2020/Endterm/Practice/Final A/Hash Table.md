Implement a hash table that uses separate chaining. You are expected to implement the following methods:

    SolutionHashTable(int capacity)
    put(String key, String value)
    remove(String key)
    get(String key)

The constructor SolutionHashTable takes as input one integer capacity and creates the hash table with the given capacity.

The method put takes as input two strings, key and value, and returns true if the entry (key, value) is successfully added to the hash table, or false otherwise.

NOTE: An entry is added successfully if the key is not null, regardless of whether an entry with that key already existed.

NOTE: If put receives a key that is already in the hash table, the method should replace the value of the entry with that key.

The method remove takes as input one string key and returns true if the entry associated with key key is successfully found and removed, or false otherwise.

The method get takes as input one string key and returns the value of the entry associated with key key in case it finds it. If the entry cannot be found, the method returns null.

Your implementation of these methods should not allow null to be used as a key.

### Template:
```java
import java.util.*;

class SolutionHashTable {
  public LinkedList<Entry>[] table;
  public int capacity;

  /**
   * Constructs a new HashTable.
   *
   * Capacity of the hash table can not be 0 or negative.
   *
   * @param capacity
   *     to be used as capacity of the table.
   * @throws IllegalArgumentException
   *     if the input capacity is invalid.
   */
  @SuppressWarnings("unchecked")
  public SolutionHashTable(int capacity) {
    // TODO
  }

  /**
   * Add a new Entry to the hash table,
   * uses separate chaining to deal with collisions.
   *
   * Returns false, if the key is null.
   *
   * @param key
   *     String representing the key of the entry.
   * @param value
   *     String representing the value of the entry.
   * @return true iff entry has been added successfully, else false.
   */
  public boolean put(String key, String value) {
    // TODO
  }

  /**
   * Retrieve the value of the entry associated with this key.
   *
   * Returns null, if the key is null.
   *
   * @param key
   *     String representing the key of the entry to look for.
   * @return value of the entry as String iff the entry with this key is found in the hash table, else null.
   */
  public String get(String key) {
    // TODO
  }

  /**
   * Remove the entry associated with this key from the hash table.
   *
   * Returns false, if the key is null.
   *
   * @param key
   *     String representing the key of the entry to remove.
   * @return true iff the entry has been successfully removed, else false.
   */
  public boolean remove(String key) {
    // TODO
  }

  /**
   * Hashes a string representing a key
   *
   * @param key
   *     String that needs to be hashed.
   * @return the hashcode of the string, modulo the capacity of the HashTable.
   */
  public int hash(String key) {
    return Math.abs(key.hashCode()) % capacity;
  }
}

```

### Library:
```java
class Entry {
  private String key;
  private String value;

  public Entry(String key, String value) {
    this.key = key;
    this.value = value;
  }

  public String getKey() {
    return key;
  }

  public String getValue() {
    return value;
  }
}

```

### Test:
```java
import static org.junit.Assert.*;

import org.junit.*;

public class UTest {
  @Test
  public void testOneElement() {
    SolutionHashTable tab = new SolutionHashTable(1);
    assertTrue(tab.put("apple", "juice"));
    assertEquals("juice", tab.get("apple"));
    assertEquals(true, tab.remove("apple"));
    assertEquals(null, tab.get("apple"));
  }

  @Test
  public void testIllegalArgument() {
    try {
      new SolutionHashTable(0);
    } catch (IllegalArgumentException e1) {
      try {
        new SolutionHashTable(-42);
      } catch (IllegalArgumentException e2) {
        return;
      }
    }
    fail();
  }
}


```

__________________________________________________________________________________________________________________

### Solution:
```java
import java.util.*;

class SolutionHashTable {
  public LinkedList<Entry>[] table;
  public int capacity;

  /**
   * Constructs a new HashTable.
   *
   * Capacity of the hash table can not be 0 or negative.
   *
   * @param capacity
   *     to be used as capacity of the table.
   * @throws IllegalArgumentException
   *     if the input capacity is invalid.
   */
  @SuppressWarnings("unchecked")
  public SolutionHashTable(int capacity) {
    if(capacity <= 0) throw new IllegalArgumentException();
    this.capacity = capacity;
    this.table = new LinkedList[capacity];
    for(int i = 0; i < capacity; i++) {
      table[i] = new LinkedList<Entry>();
    }
    
  }

  /**
   * Add a new Entry to the hash table,
   * uses separate chaining to deal with collisions.
   *
   * Returns false, if the key is null.
   *
   * @param key
   *     String representing the key of the entry.
   * @param value
   *     String representing the value of the entry.
   * @return true iff entry has been added successfully, else false.
   */
  public boolean put(String key, String value) {
      if(key == null) return false;
      if(get(key) != null) remove(key);
      Entry e = new Entry(key, value);
      table[hash(key)].add(e);
      return true;
  }

  /**
   * Retrieve the value of the entry associated with this key.
   *
   * Returns null, if the key is null.
   *
   * @param key
   *     String representing the key of the entry to look for.
   * @return value of the entry as String iff the entry with this key is found in the hash table, else null.
   */
  public String get(String key) {
    if(key == null) return null;
    int hash = hash(key);
    for(Entry e: table[hash]) {
          if(e.getKey().equals(key)) return e.getValue();
    }  
    return null;
  }

  /**
   * Remove the entry associated with this key from the hash table.
   *
   * Returns false, if the key is null.
   *
   * @param key
   *     String representing the key of the entry to remove.
   * @return true iff the entry has been successfully removed, else false.
   */
  public boolean remove(String key) {
   if(key == null) return false;
   if (get(key) != null) {
      if (get(key) == null) return false;
 
      int hash = hash(key);
      for (Entry e : table[hash]) {
        if (e.getKey().equals(key)) {
          table[hash].remove(e);
          return true;
        }
      }
    }
    return false;
   }

  /**
   * Hashes a string representing a key
   *
   * @param key
   *     String that needs to be hashed.
   * @return the hashcode of the string, modulo the capacity of the HashTable.
   */
  public int hash(String key) {
    return Math.abs(key.hashCode()) % capacity;
  }
}


```
