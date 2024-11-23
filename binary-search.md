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