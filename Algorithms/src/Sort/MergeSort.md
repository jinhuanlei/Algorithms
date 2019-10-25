## Merge Sort
Given an array of integers, sort the elements in the array in ascending order. The merge sort algorithm should be used to solve this problem.

### Examples
```
{1} is sorted to {1}
{1, 2, 3} is sorted to {1, 2, 3}
{3, 2, 1} is sorted to {1, 2, 3}
{4, 2, -3, 6, 1} is sorted to {-3, 1, 2, 4, 6}
```

### Corner Cases

* What if the given array is null? In this case, we do not need to do anything.
* What if the given array is of length zero? In this case, we do not need to do anything.

###  Solution
```java
// time NlogN
// space N + logN
public class Solution {
  public int[] mergeSort(int[] array) {
  	if(array == null || array.length == 0){
  		return array;
  	}
  	int[] helperArr = new int[array.length];
  	mergeSortHelper(array, helperArr, 0, array.length - 1);
  	return array;
  }

  public void mergeSortHelper(int[] arr, int[] helperArr, int head, int tail){
  	if(head == tail){
  		return;
  	}
  	int mid = (head + tail) / 2;
  	mergeSortHelper(arr, helperArr, head, mid);
  	mergeSortHelper(arr, helperArr, mid + 1, tail);
  	merge(arr, helperArr, head, mid, tail);
  }

  public void merge(int[] arr, int[] helperArr, int head, int mid, int tail){
  	for(int x = head; x <= tail; x++){
  		helperArr[x] = arr[x];
  	}
  	int left = head;
  	int right = mid + 1;
  	int curIndex = head;
  	while(left <= mid && right <= tail){
  		if(helperArr[left] < helperArr[right]){
  			arr[curIndex++] = helperArr[left++];
  		}else{
  			arr[curIndex++] = helperArr[right++];
  		}
  	}
  	while(left <= mid){
  		arr[curIndex++] = helperArr[left++];
  	}
  }
}
```
