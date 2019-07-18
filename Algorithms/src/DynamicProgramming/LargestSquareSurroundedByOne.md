## Largest Square Surrounded By One
Determine the largest square surrounded by 1s in a binary matrix 
(a binary matrix only contains 0 and 1), return the length of the largest square.

#### Assumptions

The given matrix is guaranteed to be of size M * N, where M, N >= 0

#### Idea
pre processing, right to left and down to up
min(left[x][y], right[x][y])是当前上左两条边的最大值.

left[x + len - 1][y] : 右边界的最大值

right[x][y + len - 1] : 下边界的最大值

#### Code
```java
public class Solution {
  public int largestSquareSurroundedByOne(int[][] matrix) {
        if(matrix.length == 0 || matrix[0].length == 0){
          return 0;
        }
        int[][] memory1 = rightLeft(matrix);
        int[][] memory2 = downUp(matrix);
        int globalMax = matrix[0][0];
        for(int x = 0; x < matrix.length; x++){
            for(int y = 0; y < matrix[0].length; y++){
                int num = Math.min(memory1[x][y], memory2[x][y]);
                for(int z = num; z >= 1; z--){
                    if((x + z - 1 < matrix.length && memory1[x + z - 1][y] >= z) && (y + z - 1 < matrix[0].length && memory2[x][y + z - 1] >= z)){
                        globalMax = Math.max(globalMax, z);
                break;
                    }
                }
            }
        }
        return globalMax;
      }

  public int[][] rightLeft(int[][] matrix) {
        int[][] memory = new int[matrix.length][matrix[0].length];
        for(int x = 0; x < matrix.length; x++) {
            // for each row
            memory[x][matrix[0].length - 1] = matrix[x][matrix[0].length - 1];
            for(int y = matrix[0].length - 2; y >= 0; y--) {
                if(matrix[x][y] == 1) {
                    memory[x][y] = memory[x][y + 1] + 1;
                } else {
                    memory[x][y] = 0;
                }
            }
        }
        return memory;
    }

    public int[][] downUp(int[][] matrix) {
        int[][] memory = new int[matrix.length][matrix[0].length];
        for(int x = 0; x < matrix[0].length; x++) {
            // for each col
            memory[matrix.length - 1][x] = matrix[matrix.length - 1][x];
            for(int y = matrix.length - 2; y >= 0; y--) {
            	if(matrix[y][x] == 1) {
                    memory[y][x] = memory[y + 1][x] + 1;
                } else {
                    memory[y][x] = 0;
                }
            }
        }
        return memory;
    }
}

```