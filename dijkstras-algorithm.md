# dijkstras
Use to find the shortest path from source to destination

* Work only for positive edge graph

### Algorithm Steps:
* Create a distance table which will store the minium distance required to reach that node from src, initially that all distances are infinite and src to src is zero.
* Add origin as distance 0.
* Till the pq is not Empty
    * Now iterate in the neighbors of cur node compare the distances to reach that neighbor with the distance array.
    * new distance = distance to reach u + edge weight (of u to v)
    * if this distance is less than the cur store distance then update the distance and add this new distance in the pq.

**Time Complexity** : O(E logV)

**Space Complexity** : O(V)
```java
public static int shortestPath(List<List<Edge>> adj, int src, int des) {
    int n = adj.size();
    int dis[] = new int[n];
    Arrays.fill(dis, Integer.MAX_VALUE);
    dis[src] = 0;

    PriorityQueue<Edge> pq = new PriorityQueue<>();
    pq.add(new Edge(src, -1, 0));

    while(!pq.isEmpty()) {
        Edge cur = pq.remove();
        int u = cur.s; 
        // u -> v
        for(Edge ne : adj.get(u)) {
            int v = ne.d;
            int wt = ne.w;
            if(dis[u] + wt < dis[v]){
                dis[v] = dis[u] + wt;
                pq.add(new Edge(v, -1, dis[v]));
            }
        }
    }
    return dis[des]==Integer.MAX_VALUE?-1:dis[des];
}
public class Edge implements Comparable<Edge>{
    int s; //source node
    int d; //destination node
    int w; // weight of the node
    public Edge(int s, int d, int w){
        this.s = s;
        this.d = d;
        this.w = w;
    }
    public int compareTo(Edge e){
        return this.w - e.w;
    }
}
```