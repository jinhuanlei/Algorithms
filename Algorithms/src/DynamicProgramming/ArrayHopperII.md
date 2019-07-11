## Array Hopper II
Given an array A of non-negative integers, you are initially positioned at index 0 of the array. A[i] means the maximum jump distance from index i (you can only jump towards the end of the array). Determine the minimum number of jumps you need to reach the end of array. If you can not reach the end of the array, return -1.

#### Assumptions

The given array is not null and has length of at least 1.
#### Examples

{3, 3, 1, 0, 4}, the minimum jumps needed is 2 (jump to index 1 then to the end of array)

{2, 1, 1, 0, 2}, you are not able to reach the end of array, return -1 in this case.


#### Analysis

M[i] represents the minimum jump from i to target

Base case : M[n - 1] = 0

Induction rule : M[i] = min(M[j]) + 1       ( i < j <= i + A[i])


#### Code
Time : N ^ 2

Space : N

```java
public class Solution {
  public int minJump(int[] array) {
    int[] memory = new int[array.length];
    memory[array.length - 1] = 0;
    for(int x = array.length - 2; x >= 0; x--){
    	int min = -1;
    	for(int y = 1; y <= array[x] && (y + x < array.length); y++){
        if(memory[y + x] != -1){
          if(min == -1 || memory[y + x] < min){
            min = memory[y + x];
          }
        }
    	}
    	memory[x] = (min == -1 ? -1 : min + 1);
    }
    return memory[0];
  }
}

```