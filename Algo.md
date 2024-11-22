# Algorithms

## Binary Search

#### Intuition 
* Is answer is continuos? means that after a value k there exits no answer.
* ask to find minimum or maximum.
* can we divide the range of value in half. After finding the mid can we reject half portion. That means we are sure that answer doesn't exits in that portion.
#### Time Complexity : O(log n)
``` java
    public int binarySearch(int arr[], int x) {
        int low = 0, high = arr.length - 1;
        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (arr[mid] == x)
                return mid;

            if (arr[mid] < x)
                low = mid + 1;

            else
                high = mid - 1;
        }
        return -1;
    }
```

## PrefixSum
``` java
    //if we have array and we have to find sum of sub-array in O(1) time
    //then we precompute prefixSum array to find sum 
    // from l to r (zero based index) 
    // sum = prefixSum[r+1]-prefix[l]
    long arr[] = new long[n];
    for(int i=0; i<n; i++) arr[i] = sc.nextLong();
    long prefixSum[] = new long[n+1];
    for(int i=0; i<n; i++){
        prefixSum[i+1] = arr[i] + prefixSum[i];
    }
    for(int i=0; i<q; i++){
        int l = sc.nextInt()-1;
        int r = sc.nextInt()-1;
       int sum  = prefixSum[r+1]-prefixSum[l];
    }
```
## Bit Manipulation
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
## Topological Sort
* To apply topoSort graph should be **DAG**(Directed Acyclic graph)
* It finds the order of the vertex.
* Topological sorting is a **dependency problem** in which completion of one task depends upon the completion of several other tasks whose order can vary.      
* Topological order may not be Unique
* u -> v (u comes before v)

    ### USING DFS
    * Perform normal dfs and pushing current node into the stack after visiting all it neighbors.
    
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

## Strongly Connected Components
## Dijkstra's Algo
## DSU
## Cycle Detection
## Sliding Window
## Two Pointer
## All Sorting Algorithms
## LCS (Longest Increasing Subsequence)
## 01 Knapsack
## MAXIMUM INTERSECTING INTERVAL
## Slow fast pointer
## Trie
## Kth largest Element
## Partition DP
## LCA