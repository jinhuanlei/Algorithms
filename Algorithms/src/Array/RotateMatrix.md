## Rotate Matrix
Rotate an N * N matrix clockwise 90 degrees.

#### Assumptions

The matrix is not null and N >= 0
#### Examples

    { {1,  2,  3}
    
      {8,  9,  4},
    
      {7,  6,  5} }

after rotation is

    { {7,  8,  1}
    
      {6,  9,  2},
    
      {5,  4,  3} }

#### Idea

Time N ^ 2

Space : N (can optimized to 1)

#### Code
```java
public class Solution {
  public void rotate(int[][] matrix) {
    if(matrix.length == 0){
    	return;
    }
    rotateHelper(matrix, matrix.length, 0);
  }

  public void rotateHelper(int[][] matrix, int size, int offset){
  	if(size < 1){
  		return;
  	}
    int len = matrix.length;
  	for(int x = 0; x < size - 1; x++){
  		// save topLeft
  		int temp = matrix[offset][x + offset];
  		// topLeft = bottomLeft
  		matrix[offset][x + offset] = matrix[len - 1 - offset - x][offset];
  		// bottomLeft = bottomRight
  		matrix[len - 1 - offset - x][offset] = matrix[len - 1 - offset][len - 1 - offset - x];
  		// bottomRight = topRight
  		matrix[len - 1 - offset][len - 1 - offset - x] = matrix[x + offset][len - 1 - offset];
  		// topRight = temp
  		matrix[x + offset][len - 1 - offset] = temp;
  	}
  	rotateHelper(matrix, size - 2, offset + 1);
  }
}
```