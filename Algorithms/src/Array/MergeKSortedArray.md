## Merge K Sorted Array
Merge K sorted array into one big sorted array in ascending order.

#### Assumptions

The input arrayOfArrays is not null, none of the arrays is null either.

#### Analysis
Maintain a minHeap with size of K, create a Element class for each of num.

Time complexity : logK * KN
Space complexity : k

#### Solution
```java
public class Solution {
	class Element{
		int col;
		int row;
		int value;
		public Element(int row ,int col, int value){
			this.col = col;
			this.row = row;
			this.value = value;
		}
	}
	public int countLen(int[][] arr){
		int len = 0;
		for(int x = 0; x < arr.length; x++){
			len += arr[x].length;
		}
		return len;
	}

	public int[] merge(int[][] arrayOfArrays) {
		int size = arrayOfArrays.length;
    		int len = countLen(arrayOfArrays);
		int[] result = new int[len];
		PriorityQueue<Element> minHeap = new PriorityQueue<>(size, new Comparator<Element>(){
			@Override
			public int compare(Element e1, Element e2){
				if(e1.value > e1.value){
					return 1;
				}else if(e1.value < e1.value){
					return -1;
				}
				return 0;
			}
		});
		for(int x = 0; x < arrayOfArrays.length; x++){
			minHeap.offer(new Element(x, 0, arrayOfArrays[x][0]));
		}
		int index = 0;
		while(!minHeap.isEmpty()){
			Element cur = minHeap.poll();
			int curRow = cur.row;
			int curCol = cur.col;
			if(cur.col < arrayOfArrays[curRow].length - 1){
				minHeap.offer(new Element(curRow, curCol + 1, arrayOfArrays[curRow][curCol + 1]));
			}
			result[index++] = cur.value;
		}
		return result;
		}
}

```