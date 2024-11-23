## Topological Sort
* To apply topoSort graph should be **DAG**(Directed Acyclic graph)
* It finds the order of the vertex.
* Topological sorting is a **dependency problem** in which completion of one task depends upon the completion of several other tasks whose order can vary.      
* Topological order may not be Unique
* u -> v (u comes before v)

    ### USING DFS
    * Perform normal dfs and push the current node into the stack after visiting all it neighbors.
    
    **Time Complexity** : O(V+E) 

    **Space Complexity** : O(V+E)
    

    ``` java
    public static List<Integer> topoSort(List<List<Integer>> adj, int V) {
        Stack<Integer> st = new Stack<>();
        boolean vis[] = new boolean[V];
        for(int i=0; i<V; i++) {
            if(!vis[i]){
                dfs(adj, vis, st, i);
            }
        }
        List<Integer> order = new ArrayList<>();
        while(!st.isEmpty()) order.add(st.pop());
        return order;
    }
    public static void dfs(List<List<Integer>> adj, boolean vis[], Stack<Integer> st,  int cur) {
        vis[cur] = true;
        for(int i=0; i<adj.get(cur).size(); i++) {
            int ne = adj.get(cur).get(i);
            if(!vis[ne]){
                dfs(adj, vis, st, ne);
            }
        }
        st.push(cur);
    }    
    ```
    ### **Khan's Algorithms**
    * Add all the edges with Indegree 0 to the Queue.
    * while queue is not Empty.
        * remove node from the queue and add this node in the answer.
        * decrease the Indegree of the neighbors (destination) node for the removed node by one.
        * if the Indegree of the destination node become zero then add that destination node in the queue.
    * If the queue is Empty and still there is node in the graph, the graph **contains cycle** and cannot be topoSorted.
     
    **Time Complexity** : O(V+E) 

    **Space Complexity** : O(V)
    ```java
        public static List<Integer> KhanAlgo(List<List<Integer>> adj, int V){
            int indegree[] = new int[V];
            for(int i=0; i<V; i++){
                for(int el : adj.get(i)){
                    indegree[el]++;
                }
            }
            Queue<Integer> q = new LinkedList<>();
            for(int i=0; i<V; i++){
                if(indegree[i]==0)q.add(i);
            }
            List<Integer> ans = new ArrayList<>();

            while(!q.isEmpty()){
                int cur = q.remove();
                ans.add(cur);
                for(int ne : adj.get(cur)){
                    indegree[ne]--;
                    if(indegree[ne]==0){
                        q.add(ne);
                    }
                }
            }

            if(ans.size()!=V){
                System.out.println("Graph Contains Cycle");
                return new ArrayList<>();
            }
            return ans;
        }

    ```
