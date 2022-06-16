# BFS on Graph
• Undiscovered – the vertex is in its initial, virgin state.

• Discovered – the vertex has been found, but we have not yet checked out
all its incident edges.

• Processed – the vertex after we have visited all of its incident edges

```java
public class Graph {
    public Map<Integer, List<int[]>> adjList;

    public int nvertices;

    public int nedges;

    public int[] degree;

    public boolean directed;



    public Graph(int v) {
        degree = new int[v];
        nvertices = v;
        nedges = 0;
        adjList = new HashMap<>();
        for(int i = 0; i < v; i++) {
            adjList.put(i, new ArrayList<>());
        }
    }

    public Graph(int v, boolean directed) {
        this(v);
        if(directed)
            this.directed = true;
    }

    public void insertEdge(int x, int y, int weight, boolean directed) {
        List<int[]> list = adjList.get(x);
        int[] tmp = new int[2];
        tmp[0] = y;
        tmp[1] = weight;
        list.add(tmp);
        adjList.put(x, list);
        if(!directed) {
            List<int[]> list2 = adjList.get(y);
            int[] tmp2 = new int[2];
            tmp2[0] = x;
            tmp2[1] = weight;
            list2.add(tmp2);
            adjList.put(y, list2);
        }
    }


    public void insertEdge(int x, int y, boolean directed) {
        insertEdge(x, y, 0, directed);
    }
}
```
```java
public class BfsGraph {
    boolean[] processed;
    boolean[] discovered;
    int[] parent;

    Graph g;

    public BfsGraph(Graph g) {
        this.g = g;
        processed = new boolean[g.nvertices];
        discovered = new boolean[g.nvertices];
        parent = new int[g.nvertices];
        for(int i = 0; i < g.nvertices; i++)
            parent[i] = -1;
    }

    public void bfs(int start) {

        Queue<Integer> q = new LinkedList<>();
        int v;
        int y;

        q.offer(start);
        discovered[start] = true;

        while (!q.isEmpty()) {
            v = q.poll();
            // process vertex early - v
            System.out.println(v);
            processed[v] = true;
            List<int[]> neighbors = g.adjList.get(v);
            for(int[] neighbor : neighbors) {
                y = neighbor[0];
                if(!processed[y] || g.directed) {
                    // process edge(v, y)
                    System.out.println(v+"-"+y);
                }
                if(!discovered[y]) {
                    q.offer(y);
                    discovered[y] = true;
                    parent[y] = v;
                }
            }
            // process vertex late - v
        }
    }

    public void processEdge(int x, int y) {
        g.nedges++;
    }

    public void findPath(int start, int end) {
        if(start == end || (end == -1))
            System.out.println(start);
        else {
            findPath(start, parent[end]);
            System.out.println(end);
        }
    }
}
```
