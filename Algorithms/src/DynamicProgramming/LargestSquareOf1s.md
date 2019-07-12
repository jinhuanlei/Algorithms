## Largest Square Of 1s
Determine the largest square of 1s in a binary matrix (a binary matrix only contains 0 and 1), return the length of the largest square.

#### Assumptions

The given matrix is not null and guaranteed to be of size N * N, N >= 0

#### Examples

{ {0, 0, 0, 0},

  {1, 1, 1, 1},

  {0, 1, 1, 1},

  {1, 0, 1, 1}}

the largest square of 1s has length of 2

#### Analysis
M[i][j] represents the largest square ith the (i, j) as the right conner

Base case : M[0][0] = 0 M[i][0] = 0  M[0][j] = 0

Induction rule : M[i][j] = 
1. 0 ==> A[i][j] = 0
1. min(M[i - 1][i - 1], M[i - 1][j], M[i][j - 1]) + 1 

#### Code
```java
public class Solution {
  public int largest(int[][] matrix) {
    int[][] memory = new int[matrix.length + 1][matrix[0].length + 1];
    int globalMax = 0;
    // init
    for(int x = 0; x <= matrix.length; x++){
    	memory[x][0] = 0;
    }
    for(int x = 0; x <= matrix[0].length; x++){
    	memory[0][x] = 0;
    }
    for(int x = 1; x <= matrix.length; x++){
    	for(int y = 1; y <= matrix[0].length; y++){
    		if(matrix[x - 1][y - 1] == 0){
    			memory[x][y] = 0;
    		}else{
    			memory[x][y] = Math.min(memory[x - 1][y - 1], Math.min(memory[x - 1][y], memory[x][y - 1])) + 1;
    		  globalMax = Math.max(globalMax, memory[x][y]);
        }
    	}
    }
    return globalMax;
  }
}

```

 