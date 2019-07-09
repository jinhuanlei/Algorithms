## Array Hopper I

Given an array A of non-negative integers, you are initially positioned at index 0 of the array. A[i] means the maximum jump distance from that position (you can only jump towards the end of the array). Determine if you are able to reach the last index.

#### Assumptions

The given array is not null and has length of at least 1.

#### Examples

{1, 3, 2, 0, 3}, we are able to reach the end of array(jump to index 1 then reach the end of the array)

{2, 1, 1, 0, 2}, we are not able to reach the end of array

#### Analysis

Time : N ^ 2

Space : N

#### Code:
```java
public class Solution {
  public boolean canJump(int[] array) {
  	boolean[] memory = new boolean[array.length];
  	memory[array.length - 1] = true;
  	for(int x = array.length - 2; x >= 0; x--){
  		for(int y = 0; y <= array[x]; y++){
  			if(x + y >= array.length){
  				break;
  			}else if(memory[x + y]){
  				memory[x] = true;
  				break;
  			}
  		}
  	}
  	return memory[0];
  }
}


```

