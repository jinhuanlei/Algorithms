## Largest And Smallest
Use the least number of comparisons to get the largest and smallest number in the given integer array. Return the largest number and the smallest number.

#### Assumptions

The given array is not null and has length of at least 1
#### Examples

{2, 1, 5, 4, 3}, the largest number is 5 and smallest number is 1. 
return [5, 1].

#### Analysis
这段代码很秀， test data : 3,2,5,4,1

step 1 : swap => 12543
step2 : 125 里找min， 543里找max

case 1 : len = 5

(len / 2, len - 1) : (2, 4)

(0, (len - 1) / 2) : (0, 2)

case 2 : len = 4

(len / 2, len - 1) : (0, 1)

(0, (len - 1) / 2) : (2, 3)


```
return new int[]{largest(array, len / 2, len - 1),smallest(array, 0, (len - 1) / 2)};
```

#### Code
```java
public class Solution {

  public int[] largestAndSmallest(int[] array) {
  	int len = array.length;
    for(int x = 0; x < len / 2; x++){
    	if(array[x] > array[len - 1 - x]){
    		swap(array, x, len - 1 - x);
    	}
    }
    return new int[]{largest(array, len / 2, len - 1),smallest(array, 0, (len - 1) / 2)};
  }

  public void swap(int[] array, int x, int y){
  	int temp = array[x];
  	array[x] = array[y];
  	array[y] = temp;
  }

  public int smallest(int[] arr, int left, int right){
  	int min = arr[left];
  	for(int x = left + 1; x <= right; x++){
  		min = Math.min(min, arr[x]);
  	}
    return min;
  }

  public int largest(int[] arr, int left, int right){
  	int max = arr[left];
  	for(int x = left + 1; x <= right; x++){
  		max = Math.max(max, arr[x]);
  	}
    return max;
  }

}

```