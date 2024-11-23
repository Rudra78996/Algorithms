# Kandane's Algorithms
## Maximum Sum Subarray 

* Take sum variable and Iterate through the given array. If the sum is greater than max sum then update max sum and if sum is less than zero then update the sum again to zero.
* As the Sum becomes less than zero it is not going to help us in maximizing  the sum value, so it is better to reject this current sum and start a new sum.  

**Time Complexity** : O(n)

**Space Complexity** : O(1)
```java
public static int maxSumSubarray(int arr[]){
    int max = Integer.MIN_VALUE;
    int sum = 0;
    for(int i=0; i<arr.length; i++) {
        sum += arr[i];
        max = Math.max(max, sum);
        if(sum < 0){
            sum = 0;
        }
    }
    return max;    
} 
```