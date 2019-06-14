## K Smallest In Unsorted Array  
  
#### Solution 1 : Min Heap  
  
#### Solution 2 : Max Heap  
  
#### Solution 3 : Quick Select  
  
 Use the idea of **Partion**  in Quick Sort. Each time find a pivot and put all the elements less than the target value to the left and put the elements that large than the target to the right.
 
 **Average time conplexity :** n + n/2 + n/4 + ... = O(N)               
 Space : O(logN)  Call stack spaces
 
 **Worst time complexity :** n + (n - 1) + (n - 2) + ... = O (N ^ 2)    
 Space : O(N)     Call stack spaces

Code:
```java  
public class Solution {
  public int[] kSmallest(int[] array, int k) {
    // Write your solution here
    if(k == 0){
      return new int[0];
    }
    int left = 0;
    int right = array.length - 1;
    int index = partition(array, left, right);;
    while(index != k - 1){
      if(index > k - 1){
        right = index - 1;
      }else if(index < k - 1){
        left = index + 1;
      }
      index = partition(array, left, right);
    }
    int[] result = new int[k];
    for(int x = 0; x < k; x++){
      result[x] = array[x];
    }
    Arrays.sort(result);
    return result;
  }

  public int partition(int[] array, int left, int right){
    int pivotIndex = getRandomIndex(left, right);
    int pivotVal = array[pivotIndex];
    swap(array, pivotIndex, right);
    int l = left;
    int r = right - 1;
    while(l <= r){
      if(array[l] < pivotVal){
        l++;
      }else if(array[r] >= pivotVal){
        r--;
      }else{
        swap(array, l++, r--);
      }
    }
    swap(array, l, right);
    return l;
  }

  public void swap(int[] arr, int left, int right){
      int temp = arr[left];
      arr[left] = arr[right];
      arr[right] = temp;
  }

  public int getRandomIndex(int left, int right){
    return left + (int)Math.random() * (right - left + 1);
  }
}

```