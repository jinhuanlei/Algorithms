## Longest Ascending SubArray
Given an unsorted array, find the length of the longest subarray in which the numbers are in ascending order.

#### Assumptions

The given array is not null
#### Examples

{7, 2, 3, 1, 5, 8, 9, 6}, longest ascending subarray is {1, 5, 8, 9}, length is 4.

{1, 2, 3, 3, 4, 4, 5}, longest ascending subarray is {1, 2, 3}, length is 3.

**Base case :** M[0] = 1

**Induction rule:**

case 1 : M[i] = M[i - 1] + 1  if arr[i] > arr[i - 1]

case 2 : M[i] = 1             if arr[i] <= arr[i - 1]

#### Solution

```java
public class Solution {
  public int longest(int[] array) {
    if(array.length == 0){
    	return 0;
    }
    int globalMax = 1;
    int curMax = 1;
    for(int x = 1; x < array.length; x++){
    	if(array[x] > array[x - 1]){
    		curMax++;
    		globalMax = Math.max(globalMax, curMax);
    	}else{
    		curMax = 1;
    	}
    }
    return globalMax;
  }
}

```
