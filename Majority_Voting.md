# Boyer-Moore Majority Voting Algorithm

Used to find the majority element among the given elements that have more than N/ 2 occurrences.

**Time Complexity** : O(n)

**Space Complexity** : O(1)

```java
public static int majorityElement(int arr[]) {
    int el = arr[0];
    int count = 0;
    for(int i=0; i<arr.length; i++) {
        if(count==0){
            el = arr[i];
            count = 1;
        }else if(arr[i]==el){
            count++;
        }else{
            count--;
        }
    }
}
```