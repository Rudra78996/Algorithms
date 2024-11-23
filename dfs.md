## DFS
#### Time Complexity : O(V+E), Space Complexity : O(V+E) 
``` java
    public void dfs(List<List<Integer>> adj, boolean vis[], int cur) {
        vis[cur] = true;
        for(int i=0; i<adj.get(cur).size(); i++) {
            int ne = adj.get(cur).get(i);
            if(!vis[ne]) {
                dfs(adj, vis, ne);
            }
        }
    }
```