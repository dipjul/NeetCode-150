# Bellman Ford Algorithm for Single Source Shortest Path

In graph theory, the Bellman-Ford (BF) algorithm is a Single Source Shortest Path (SSSP) algorithm. This means it can find the shortest path from one node to any other node.However, BF is not ideal for most SSSP problems because it has a time complexity of O(EV). It is better to use Dijkstra’s algorithm which is much faster. It is on the order of Θ((E+V)log(V)) when using a binary heap priority queue.

However, Dijkstra’s algorithm can fail when the graph has negative edge weights. This is when BF becomes really handy because it can be used to detect negative cycles and determine where they occur.Finding negative cycles can be useful in many types of applications. One particularly neat application arises in finance when performing an arbitragebetween two or more markets.

## Approach
```

```
```java
public class BellmanFordEdgeList {

  // A directed edge
  public static class Edge {
    double cost;
    int from, to;

    public Edge(int from, int to, double cost) {
      this.to = to;
      this.from = from;
      this.cost = cost;
    }
  }

  /**
   * An implementation of the Bellman-Ford algorithm. The algorithm finds the shortest path between
   * a starting node and all other nodes in the graph. The algorithm also detects negative cycles.
   * If a node is part of a negative cycle then the minimum cost for that node is set to
   * Double.NEGATIVE_INFINITY.
   *
   * @param edges - An edge list containing directed edges forming the graph
   * @param V - The number of vertices in the graph.
   * @param start - The id of the starting node
   */
  public static double[] bellmanFord(Edge[] edges, int V, int start) {

    double[] dist = new double[V];
    java.util.Arrays.fill(dist, Double.POSITIVE_INFINITY);
    dist[start] = 0;

    // Only in the worst case does it take V-1 iterations for the Bellman-Ford
    // algorithm to complete. Another stopping condition is when we're unable to
    // relax an edge, this means we have reached the optimal solution early.
    boolean relaxedAnEdge = true;

    // For each vertex, apply relaxation for all the edges
    for (int v = 0; v < V - 1 && relaxedAnEdge; v++) {
      relaxedAnEdge = false;
      for (Edge edge : edges) {
        if (dist[edge.from] + edge.cost < dist[edge.to]) {
          dist[edge.to] = dist[edge.from] + edge.cost;
          relaxedAnEdge = true;
        }
      }
    }

    // Run algorithm a second time to detect which nodes are part
    // of a negative cycle. A negative cycle has occurred if we
    // can find a better path beyond the optimal solution.
    relaxedAnEdge = true;
    for (int v = 0; v < V - 1 && relaxedAnEdge; v++) {
      relaxedAnEdge = false;
      for (Edge edge : edges) {
        if (dist[edge.from] + edge.cost < dist[edge.to]) {
          dist[edge.to] = Double.NEGATIVE_INFINITY;
          relaxedAnEdge = true;
        }
      }
    }

    // Return the array containing the shortest distance to every node
    return dist;
  }
}
```

## Complexity Analysis
```
- Time Complexity: O(V*E)
- Space Complexity: O(V)
```
