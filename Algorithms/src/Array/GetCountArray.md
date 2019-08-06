## Get Count Array
Given an array A of length N containing all positive integers from [1...N]. How to get an array B such that B[i] represents how many elements A[j] (j > i) in array A that are smaller than A[i].

#### Assumptions:

The given array A is not null.
#### Examples:

A = { 4, 1, 3, 2 }, we should get B = { 3, 0, 1, 0 }.
#### Requirement:

time complexity = O(nlogn).

#### Solution

Using helper array to sort the index array, during the process, 
do the counter operations.

```java
public class Solution {
  public int[] countArray(int[] array) {
    int[] helper = new int[array.length];
    int[] indexArr = getIndexArray(array);
    int[] result = new int[array.length];
    mergeSort(array, helper, indexArr, result, 0, array.length - 1);
    return result;
  }

  public void mergeSort(int[] array, int[] helper, int[] indexArr, int[] result, int left, int right){
  	if(left >= right){
  		return;
  	}
  	int mid = left + (right - left) / 2;
  	mergeSort(array, helper, indexArr, result, left, mid);
  	mergeSort(array, helper, indexArr, result, mid + 1, right);
  	merge(array, helper, indexArr, result, left, mid, right);
  }

  public void merge(int[] array, int[] helper, int[] indexArr, int[] result, int left, int mid, int right){
  	copyArray(helper, indexArr, left, right);
  	int curLeft = left;
  	int curRight = mid + 1;
  	int cur = left;
  	while(curLeft <= mid){
  		if(curRight > right || array[helper[curLeft]] <= array[helper[curRight]]){
  			result[helper[curLeft]] += (curRight - mid - 1);
  			indexArr[cur++] = helper[curLeft++];
  		}else{
  			indexArr[cur++] = helper[curRight++];
  		}
  	}
  }

  public void copyArray(int[] helper, int[] indexArr, int left, int right){
  	for(int x = left; x <= right; x++){
  		helper[x] = indexArr[x];
  	}
  }

  public int[] getIndexArray(int[] array){
  	int[] result = new int[array.length];
  	for(int x = 0; x < result.length; x++){
  		result[x] = x;
  	}
  	return result;
  }
}

```