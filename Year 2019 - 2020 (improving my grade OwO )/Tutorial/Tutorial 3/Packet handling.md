Packets are important for sending information online, for example when you want to look at pictures of snails, you will obtain packets containing information that when combined together can result in a picture of a snail.

A simplified explanation of how packets work is:
1. Some information gets split into packets of a certain size, where each packet will get an id (sequence number)
2. Each packet gets sent to the receiver
3. The receiver will receive these packets in no particular order, as some packets might take longer to arrive
4. The receiver will use the id (sequence number) to correctly order the packets to obtain the complete message

In this exercise, you will help out with correctly receiving these packets and putting them in the correct order.
This will be done in the method processPacket(Packet p), you will receive one packet at a time, each time you receive a packet you should either return null if you haven’t collected all packets yet, otherwise return the packets in the correct order.

The implementation of a packet can be found in the library. Each packet has the following information:

    amount - the total number of packets
    id - the sequence number of this packet
    msg - the payload of the packet

### Library
```java
import java.util.*;

class Packet {

  private int amount;

  private int id;

  private String msg;

  /**
   * Creates a new packet
   *
   * @param amount - the number of packets in total
   * @param id - the identifier (sequence number) of this packet
   * @param msg - the message (payload) of this packet
   */
  public Packet(int amount, int id, String msg) {
    this.amount = amount;
    this.id = id;
    this.msg = msg;
  }

  /**
   * @return Id (sequence number) of this packet
   */
  public int getId() {
    return this.id;
  }

  public int getAmount() {
    return this.amount;
  }

  /**
   * @return Message (payload) of this packet
   */
  public String getMsg() {
    return this.msg;
  }

  /**
   * @return String encoding of this packet
   */
  public String toString() {
    return this.id + ": " + this.msg;
  }

  @Override
  public boolean equals(Object o) {
    if (this == o) {
      return true;
    }
    if (o instanceof Packet) {
      Packet other = (Packet) o;
      if (this.id == other.id) {
        if (this.msg.equals(other.msg)) {
          return true;
        }
      }
    }
    return false;
  }

  @Override
  public int hashCode() {
    return this.getId();
  }
}

class Util {

  /**
   * Given a String message and an integer representing the size of each packet,
   * the message will be split into separate packets and returned as a list.
   *
   * If the message is not divisible by packetSize, additional zeros will be used to pad the message.
   *
   * @param msg
   * @param packetSize
   * @return
   */
  public static List<Packet> createPackets(String msg, int packetSize) {
    List<Packet> res = new ArrayList<>();
    int n = msg.length();
    int remainder = n % packetSize;
    for (int i = 0; i < packetSize - remainder; i++) {
      msg += "0";
    }
    int packets = n / packetSize + (remainder == 0 ? 0 : 1);
    for (int i = 0; i < packets; i++) {
      res.add(new Packet(packets, i, msg.substring(i * packetSize, i * packetSize + packetSize)));
    }
    return res;
  }
}

```

### Solution
```java
class PacketHandler {
  Packet[] packets;
  int size;
  
  public PacketHandler() {
    this.packets = null;
    this.size = 0;
  }

  /**
   * Processes a packet received from a sender by storing it,
   * if all expected packets have been received, the packets will be returned in the correct order by their ID.
   * If not all packets have been received, this method will return null.
   *
   * The packet handler will reset itself after returning the packets.
   *
   * @param p
   *     - the packet that needs to be processed
   * @return list of all packets in the correct order if all packets have been received, else null.
   */
  public Packet[] processPacket(Packet p) {
    if (packets == null) packets = new Packet[p.getAmount()];
    packets[p.getId()] = p;
    size++;
    if (size == p.getAmount()) return packets;
    return null;
  }
}



```
