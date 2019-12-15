### Hash functions (1/6)
Implement four child classes of the abstract HashTable as defined in the previous exercise with different hashing methods.
In this representation b0 is the starting value and bi are the intermediate values of the hash code for the string up to character i.
s represents the size of the table.
n represents the length of the String.
ci is the (integer) value of the ith character of the String, where 1≤i≤n (the first character is at c1 unlike in Java).
The final value is given as H:

- A variant on the ETH algorithm:
  b0=1
  bi=ci∗((bi−1mod257)+1)
  H=bnmods

- A variant on the GNU-cpp algorithm:
  b0=0
  bi=4bi−1+ci
  H=(the last 31 bits of bn)mods

- A variant on the GNU-cc1 algorithm:
  b0=n
  bi=613bi−1+ci
  H=(the last 30 bits of bn)mods

- The hashCode() method of the Java String class. If this is negative, make it positive by using Math.abs() and put it in the right range by using the modulus operator.

```java
class ETHHash extends HashTable {
  public ETHHash(int size) {
    super(size);
  }

  @Override
  public int hash(String item) {
    if(item == null) return 0;
    int b = 1;
    for(int i =0; i < item.length(); i++){
      b = item.charAt(i) * ((b % 257) +1);
    }
    return b % getCapacity();
  }
}

class GNUCPPHash extends HashTable {
  public GNUCPPHash(int size) {
    super(size);
  }

  @Override
  public int hash(String item) {
    if(item == null) return 0;
    int b =0;
    for(int i=0; i < item.length(); i++) {
      b = 4 * b + item.charAt(i);
    }
    return (((1  << 31) - 1) & b) % getCapacity();
  }
}

class GNUCC1Hash extends HashTable {
  public GNUCC1Hash(int size) {
    super(size);
  }

  @Override
  public int hash(String item) {
    if(item == null) return 0;
    int b = item.length();
    for(int i =0; i<item.length(); i++) {
      b = 613*b + item.charAt(i);
    }
    return (((1 << 30) - 1) & b ) % getCapacity();
  }
}

class HashCodeHash extends HashTable {
  public HashCodeHash(int size) {
    super(size);
  }

  @Override
  public int hash(String item) {
    if(item == null) return 0;
    return Math.abs(item.hashCode()) % getCapacity();
  }
}
```
