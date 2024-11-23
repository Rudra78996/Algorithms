## BFS
**Time Complexity** : O(V+E) max of number of vertex or edge.

**Space Complexity** : O(v+E)
``` java
    public void bfs(List<List<Integer>> adj, int src) {
        boolean vis[] = new boolean[adj.size()];
        Queue<Integer> q = new LinkedList<>();
        q.add(src);
        vis[src] = true;
        while(!q.isEmpty()) {
            int t = q.size();
            while(t-->0){
                int cur = q.remove();
                for(int i=0; i<adj.get(cur).size(); i++) {
                    int ne = adj.get(cur).get(i);
                    if(!vis[ne]) {
                        q.add(ne);
                        vis[ne] = true;
                    }
                }
            }
        }
    }
```