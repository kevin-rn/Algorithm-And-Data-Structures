You love listening to music just as much as everyone else, but with platforms like Spotify and Youtube you find it
difficult to enjoy your ADS (Algorithmic Daily Songs) playlist as there are way too many advertisements interrupting your songs.
Since you have been following an algorithmic course for 3 weeks now, you feel confident in your programming skills
and decide to implement your own music app. In order for your app to function correctly you need a playlist which you
can listen to, skip songs and go back once you’ve realized you have skipped your favourite song. For this purpose we have provided you the structure of your playlist class and all you have to do is implement the required methods so you can enjoy your playlist without interruptions.

An important note is that you are not allowed to use any additional data structures different from the ones we give you in the visible library.

Hint: What data structure to use?
In order to keep track of the current song you are playing and the list of songs you are yet to play and the ones you have already played you need an appropriate datastructures in which you will store the songs. To give you a headstart we have provided you with an implementation of a LibraryStack and LibraryQueue. It's your task to figure out how you can make use of them. 

### Library:
```java
import java.util.*;

class LibraryStack {

  List<String> items;

  public LibraryStack() {
    items = new ArrayList<>();
  }

  public boolean isEmpty() {
    return this.items.isEmpty();
  }

  public void push(String s) {
    this.items.add(s);
  }

  public String pop() {
    return this.items.remove(this.items.size() - 1);
  }

  public String top() {
    return this.items.get(this.items.size() - 1);
  }
}

class LibraryQueue {

  List<String> items;

  public LibraryQueue() {
    items = new ArrayList<>();
  }

  public boolean isEmpty() {
    return this.items.isEmpty();
  }

  public void enqueueFront(String s) {
    this.items.add(0, s);
  }

  public void enqueueBack(String s) {
    this.items.add(s);
  }

  public String dequeue() {
    return this.items.remove(0);
  }

  public String first() {
    return this.items.get(0);
  }
}
```

### Official solution:
```java
class PlayList {

  private LibraryStack stack;

  private LibraryQueue queue;

  private String current;

  /**
   * Constructor of the playlist, creates a playlist with the given songs.
   * @param songs - the songs that will be part of this playlist
   */
  public PlayList(String[] songs) {
    this.stack = new LibraryStack();
    this.queue = new LibraryQueue();
    this.current = null;
    for (String s : songs) {
      this.queue.enqueueBack(s);
    }
  }

  /**
   * Starts playing the first song in the playlist, if no songs was playing yet.
   * @return the first song that will be played if no song was playing, otherwise null
   */
  public String playSong() {
    if (this.current == null) {
      this.current = this.queue.dequeue();
      return this.current;
    }
    return null;
  }

  /**
   * Switches to the next song in the playlist.
   * @return the next song in the playlist
   */
  public String nextSong() {
    this.stack.push(this.current);
    this.current = this.queue.dequeue();
    return this.current;
  }

  /**
   * Switches back to the previous song in the playlist.
   * @return the previous song in the playlist
   */
  public String previousSong() {
    this.queue.enqueueFront(this.current);
    this.current = this.stack.pop();
    return this.current;
  }
}

```

### My Solution:
```java
class PlayList {
  String[] songs;
  int i;

  /**
   * Constructor of the playlist, creates a playlist with the given songs.
   * @param songs - the songs that will be part of this playlist
   */
  public PlayList(String[] songs) {
    this.songs = songs;
    i = 0;
  }

  /**
   * Starts playing the first song in the playlist, if no songs was playing yet.
   * @return the first song that will be played if no song was playing, otherwise null
   */
  public String playSong() {
    if(i != 0) return null;
    return songs[i];
  }

  /**
   * Switches to the next song in the playlist.
   * @return the next song in the playlist
   */
  public String nextSong() {
    return songs[++i];
  }

  /**
   * Switches back to the previous song in the playlist.
   * @return the previous song in the playlist
   */
  public String previousSong() {
    return songs[--i];
  }
}


```
