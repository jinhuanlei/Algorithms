## Spiral Order Traverse II
Traverse an M * N 2D array in spiral order clock-wise starting from the top left corner. Return the list of traversal sequence.

#### Assumptions

The 2D array is not null and has size of M * N where M, N >= 0
#### Examples

{ {1,  2,  3,  4},

  {5,  6,  7,  8},

  {9, 10, 11, 12} }

the traversal sequence is [1, 2, 3, 4, 8, 12, 11, 10, 9, 5, 6, 7]
#### Idea
recursion记录长和宽, 还有offset

#### Code
```java
public class Solution {
  public List<Integer> spiral(int[][] matrix) {
    List<Integer> result = new ArrayList<>();
    spiralHelper(matrix, result, matrix.length, matrix[0].length, 0);
    return result;
  }
  public void spiralHelper(int[][] matrix, List<Integer> result, int rowSize, int colSize, int offset){
  	if(rowSize <= 0 || colSize <= 0){
  		return;
  	}if(rowSize == 1){
      for(int x = 0; x < colSize; x++){
  		  result.add(matrix[offset][x + offset]);
  	  }
      return;
    }else if(colSize == 1){
      for(int x = 0; x < rowSize; x++){
  		  result.add(matrix[x + offset][colSize + offset - 1]);
  	  }
      return;
    }
  	// up
  	for(int x = 0; x < colSize - 1; x++){
  		result.add(matrix[offset][x + offset]);
  	}
  	// right
  	for(int x = 0; x < rowSize - 1; x++){
  		result.add(matrix[x + offset][colSize + offset - 1]);
  	}
  	//down
  	for(int x = colSize - 1; x > 0; x--){
  		result.add(matrix[rowSize + offset - 1][offset + x]);
  	}
  	//left
  	for(int x = rowSize - 1; x > 0; x--){
  		result.add(matrix[x + offset][offset]);
  	}
    spiralHelper(matrix, result, rowSize - 2, colSize - 2, offset + 1);
  }
}

```