Implement method countVertices, which takes a graph and a vertex as input, and returns the number of vertices in the same connected component of the given vertex.

Your implementation needs to use depth-first search (DFS).

The method should return 0, if the graph or vertex is null.

### Template:
```java
import java.util.*;

class Solution {
  /**
   * Counts the number of vertices in the same connected component as v in graph g.
   * This is done using depth first search.
   *
   * Returns 0 if the graph or vertex is null
   *
   * @param g
   *     The graph to count vertices in.
   * @param v
   *     The vertex to start counting at.
   * @return the number of vertices in the same connected component.
   */
  public static int countVertices(Graph g, Graph.Vertex v) {
    // TODO
  }
}
```

### Library:
```java
class Graph {
  static class Vertex {
    private int id;
    private Set<Vertex> neighbours;

    public Vertex(int id) {
      this.id = id;
      neighbours = new HashSet<>();
    }

    public void addNeighbour(Vertex v) {
      neighbours.add(v);
    }

    private Collection<Vertex> getNeighbours() {
      return new ArrayList<>(this.neighbours);
    }

    public int getId() {
      return this.id;
    }
  }

  Map<Integer, Vertex> vertices;

  public Graph() {
    this.vertices = new HashMap<>();
  }

  public void addVertex(Vertex v) {
    this.vertices.put(v.getId(), v);
  }

  public Collection<Vertex> getAllVertices() {
    return new ArrayList<>(this.vertices.values());
  }

  public List<Vertex> getNeighbours(Vertex v) {
    List<Vertex> neigh = new ArrayList<>(((Vertex) v).getNeighbours());
    return neigh;
  }

  public void addEdge(Vertex v, Vertex w) {
    v.addNeighbour(w);
    w.addNeighbour(v);
  }
}

```

### Test:
```java
import static org.junit.Assert.*;

import org.junit.*;

public class UTest {
  @Test
  public void testNull() {
    Graph g = new Graph();
    Graph.Vertex v = null;
    assertEquals(0, Solution.countVertices(g, v));
    g = null;
    v = new Graph.Vertex(1);
    assertEquals(0, Solution.countVertices(g, v));
  }

  @Test
  public void testExample() {
    Graph g = new Graph();
    Graph.Vertex v = new Graph.Vertex(1);
    Graph.Vertex w = new Graph.Vertex(2);
    Graph.Vertex x = new Graph.Vertex(3);
    Graph.Vertex y = new Graph.Vertex(4);
    g.addVertex(v);
    g.addVertex(w);
    g.addVertex(x);
    g.addVertex(y);
    g.addEdge(v, w);
    g.addEdge(w, y);
    assertEquals(3, Solution.countVertices(g, v));
    assertEquals(3, Solution.countVertices(g, w));
    assertEquals(3, Solution.countVertices(g, y));
    assertEquals(1, Solution.countVertices(g, x));
  }
}

```

___________________________________________________________________________________________________________
### Solution:
```java
import java.util.*;

class Solution {
  /**
   * Counts the number of vertices in the same connected component as v in graph g.
   * This is done using depth first search.
   *
   * Returns 0 if the graph or vertex is null
   *
   * @param g
   *     The graph to count vertices in.
   * @param v
   *     The vertex to start counting at.
   * @return the number of vertices in the same connected component.
   */
  public static int countVertices(Graph g, Graph.Vertex v) {
    if(g == null || v == null) return 0;
    Stack<Graph.Vertex> q = new Stack<>();
    Set<Graph.Vertex> known = new HashSet<>();
    q.add(v);
    
    while(!q.isEmpty()) {
      Graph.Vertex c = q.pop();
      known.add(c);
      for(Graph.Vertex n : g.getNeighbours(c)) {
        if(!known.contains(n)) q.add(n);
      }
    }
    return known.size();
  }
}
```
