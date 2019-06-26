## ReOrder Array
* Description

Given an array of elements, reorder it as follow:

{ N1, N2, N3, …, N2k } → { N1, Nk+1, N2, Nk+2, N3, Nk+3, … , Nk, N2k }

{ N1, N2, N3, …, N2k+1 } → { N1, Nk+1, N2, Nk+2, N3, Nk+3, … , Nk, N2k, N2k+1 }

Try to do it in place.

* Assumptions

The given array is not null
* Examples

{ 1, 2, 3, 4, 5, 6} → { 1, 4, 2, 5, 3, 6 }

{ 1, 2, 3, 4, 5, 6, 7, 8 } → { 1, 5, 2, 6, 3, 7, 4, 8 }

{ 1, 2, 3, 4, 5, 6, 7 } → { 1, 4, 2, 5, 3, 6, 7 }

* Case 1 : size 是奇数  => 忽略最后一个值

* Case 2 : size 是偶数

    * Case 2.1 : size / 2 是偶数

    * Case 2.2 : size / 2 是奇数

Code:
```java
public class Solution {
  public int[] reorder(int[] array) {
    if(array.length <= 1){
      return array;
    }
    if(array.length % 2 == 0){
      reorderHelper(array, 0, array.length - 1);
    }else{
      reorderHelper(array, 0, array.length - 2);
    }
    return array;
  }

  public void reorderHelper(int[] array, int left, int right){
    if(right - left <= 1){
      return;
    }
    int size = right - left + 1;
    int mid = left + size / 2;
    int leftMid = left + size / 4;
    int rightMid = mid + size / 4;
    reverse(array, leftMid, mid - 1);
    reverse(array, mid, rightMid - 1);
    reverse(array, leftMid, rightMid - 1);
    reorderHelper(array, left, left + (leftMid - left) * 2 - 1);
    reorderHelper(array, left + (leftMid - left) * 2 - 1 + 1, right);
  }

  public void reverse(int[] arr, int left, int right){
    while(left < right){
      swap(arr, left++, right--);
    }
  }

  public void swap(int[] arr, int left, int right){
    int temp = arr[left];
    arr[left] = arr[right];
    arr[right] = temp;
  }
}

```