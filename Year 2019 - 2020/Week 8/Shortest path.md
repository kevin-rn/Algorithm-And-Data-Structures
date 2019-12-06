### Shortest Path
Implement a method shortestPath(g, v, u) that finds the shortest path (least number of edges) between nodes v and u and returns this path in the form of a list of nodes.

NOTE: v and u should be included in this list (see the tests for examples).

The following two interfaces are provided, which have full implementations in the hidden library code.

  interface Vertex {
    int getId();
  }

  interface Graph {
    // Gets neighbours of v in this Graph, ordered by id
    public List<Vertex> getNeighbours(Vertex v);
    // Gets all vertices of this Graph
    public Collection<Vertex> getAllVertices();
  }
  
 The hidden library code also has a full implementation of the breadth first version of the iterator from the first assignment. 
 This iterator can be instantiated using new GraphIterator(Graph g, Vertex v). 
 Furthermore, note that the iterator implements the Iterator<Vertex> interface, whose description can be found in the Java API documentation.

IMPORTANT: You are required to use the given breadth-first GraphIterator in your solution. 
In an exam setting, your code will be checked and if it is seen that you do not use it, your grade will be overridden to 1.

Again, you cannot label nodes or edges. Instead, you need to maintain discovered edges in a map predecessors, which stores the keys of a map in a height-balanced search tree.   
It can be instantiated with Map<Vertex, Vertex> predecessors = new TreeMap<>();.  
To remember node v was discovered from node w, you call predecessors.put(v, w).   
To check wether node v was already discovered, you call predecessors.containsKey(v).   
To access the predecessor of node v, you call predecessors.get(v).  

```java
import java.util.*;

class Solution {
  /**
   * Find the shortest path between v and u in the graph g.
   *
   * @param g
   *     graph to search in.
   * @param v
   *     node to start from.
   * @param u
   *     node to reach.
   * @return the nodes you that form the shortest path, including v and u. An
   * empty list iff there is no path between v and u.
   */
  public static List<Vertex> shortestPath(Graph g, Vertex v, Vertex u) {
    LinkedList<Vertex> path = new LinkedList<>();
    Iterator<Vertex> it = new GraphIterator(g,v);
    
    while (it.hasNext())  {
      Vertex x = it.next();
      path.add(x);
      if (x == u) break;
    }
    
    //no path at all
    if (path.get(path.size() - 1) != u)  return new ArrayList<>();
    
    List<Vertex> shortest = new ArrayList<>();
    int i = path.size() - 1;
    
    while (true) {
      Vertex c = path.get(i);
      List<Vertex> connected = g.getNeighbours(c);
      shortest.add(c);
      
      if (c == v)  {
        Collections.reverse(shortest);
        return shortest;
      }
      
      int index = 0;
      for (Vertex vertex : path) {
        if (!shortest.contains(vertex) && connected.contains(vertex)) {
          i = index;
          break;
        }
        index++;
      }
    }
  }
}
```
