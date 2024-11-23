## PrefixSum
* if we have array and we have to find sum of sub-array (l, r) in O(1) time.
* then we precompute prefixSum array. 
* for l to r (zero based index) 
* sum = prefixSum[r+1]-prefix[l]
 
``` java
    public static void prefixSum(int arr[]){
        int n = arr.length;
        long prefixSum[] = new long[n+1];
        for(int i=0; i<n; i++){
            prefixSum[i+1] = arr[i] + prefixSum[i];
        }
        for(int i=0; i<q; i++){
            int l = sc.nextInt()-1;
            int r = sc.nextInt()-1;
            int sum  = prefixSum[r+1]-prefixSum[l];
        }
    }
```