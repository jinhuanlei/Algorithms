## Quick Sort
Given an array of integers, sort the elements in the array in ascending order. The quick sort algorithm should be used to solve this problem.

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

### Solution
```java
public class Solution {
	public int[] quickSort(int[] array) {
		if(array == null || array.length == 0){
			return array;
		}
		quickSortHelper(array, 0 , array.length - 1);
		return array;
	}

	public void quickSortHelper(int[] arr, int head, int tail){
		if(head >= tail){
			return;
		}
		int pivot = partition(arr, head, tail);
		quickSortHelper(arr, head, pivot - 1);
		quickSortHelper(arr, pivot + 1, tail);
	}

	public int  partition(int[] arr, int head, int tail){
		int pivotIndex = getRandomPivot(head, tail);
		int pivotValue = arr[pivotIndex];
		swap(arr, pivotIndex, tail);
		int left = head;
		int right = tail - 1;
		while(left <= right){
			if(arr[left] < pivotValue){
				left++;
			}else if(arr[right] >= pivotValue){
				right--;
			}else{
			  swap(arr, left++, right--);
      }
		}
		swap(arr, tail, left);
    return left;
	}

	public void swap(int[] arr,int left,int right){
        int x = arr[left];
        arr[left] = arr[right];
        arr[right] = x;
    }

	public int getRandomPivot(int head, int tail){
		return head + (int)(Math.random() * (tail - head + 1));
	}
}

```