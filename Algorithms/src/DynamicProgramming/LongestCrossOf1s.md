## Longest Cross Of 1s
Given a matrix that contains only 1s and 0s, find the largest cross which contains only 1s, with the same arm lengths and the four arms joining at the central point.

Return the arm length of the largest cross.

#### Assumptions

The given matrix is not null, has size of N * M, N >= 0 and M >= 0.
#### Examples

    { {0, 0, 0, 0},
    
      {1, 1, 1, 1},
    
      {0, 1, 1, 1},
    
      {1, 0, 1, 1} }

the largest cross of 1s has arm length 2.

#### Analysis
Solution1 : BruteForce 

    for for:
        check Up, Down, Left,Right to check its max availability
    Time : N ^ 3
    Space : 1
    
Solution 2 : DP

    pre processing, 
    left to right, right to left, up to down, down to up with the maxsize of 1s
    M[i][j] current max length of 1s
    indextuon rule: for for( max(globalMax, min(four memory array[x][y])) )
    Time : N ^ 2
    space N ^ 2
        

    
#### Code
```java
public class Solution {
    public int largest(int[][] matrix) {
        if(matrix.length == 0 || matrix[0].length == 0) {
            return 0;
        }
        int[][] memoryLeftRight = leftRight(matrix);
        int[][] memoryRightLeft = rightLeft(matrix);
        int[][] memoryUpDown = upDown(matrix);
        int[][] memoryDownUp = downUp(matrix);
        int globalMax = matrix[0][0];
        for(int x = 0; x < matrix.length; x++) {
            for(int y = 0; y < matrix[0].length; y++) {
                int min1 = Math.min(memoryLeftRight[x][y], memoryRightLeft[x][y]);
                int min2 = Math.min(memoryUpDown[x][y], memoryDownUp[x][y]);
                globalMax = Math.max(globalMax, Math.min(min1, min2));
            }
        }
        return globalMax;
    }

    public int[][] leftRight(int[][] matrix) {
        int[][] memory = new int[matrix.length][matrix[0].length];
        for(int x = 0; x < matrix.length; x++) {
            // for each row
            memory[x][0] = matrix[x][0];
            for(int y = 1; y < matrix[0].length; y++) {
                if(matrix[x][y] == 1) {
                    memory[x][y] = memory[x][y - 1] + 1;
                } else {
                    memory[x][y] = 0;
                }
            }
        }
        return memory;
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

    public int[][] upDown(int[][] matrix) {
        int[][] memory = new int[matrix.length][matrix[0].length];
        for(int x = 0; x < matrix[0].length; x++) {
            // for each col
            memory[0][x] = matrix[0][x];
            for(int y = 1; y < matrix.length; y++) {
            	if(matrix[y][x] == 1) {
                    memory[y][x] = memory[y - 1][x] + 1;
                } else {
                    memory[y][x] = 0;
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