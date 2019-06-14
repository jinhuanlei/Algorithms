## K Smallest In Unsorted Array  
  
#### Solution 1 : Min Heap  (**Offline Algorithm)**
  Step 1 : Built a heap with size of N --- O(N)
  
  Step 2 : Poll K elements from this Heap --- O(KlogN)
  
  Time : O(N + KlogN)
  
  The code here did not implement with heapify, so the first step it takes O(NlogN).
 
 Code:
  ```java
public class Solution {
  public int[] kSmallest(int[] array, int k) {
    // Min heap
    if(k == 0){
      return new int[k];
    }
    PriorityQueue<Integer> minHeap = new PriorityQueue<>();
    for(int x = 0; x < array.length; x++){
      minHeap.offer(array[x]);
    }
    int[] result = new int[k];
    for(int x = 0; x < k; x++){
      result[x] = minHeap.poll();
    }
    return result;
  }
}
```
#### Solution 2 : Max Heap  (**Online Algorithm)**
  Step 1 : Maintain a PriorityQueue with size of K --- O(K)
  
  Step 2 : Traverse the rest of elements, if current element is less than the value of heap top we do enqueue. Otherwise we skip the element. --- O((N - k)logK)
  
  Time : O(K + (N - k)logK)
  
  Code:
  ```java
public class Solution {
  public int[] kSmallest(int[] array, int k) {
    if(k == 0){
      return new int[0];
    }
    PriorityQueue<Integer> maxHeap = new PriorityQueue<>(k , new Comparator<Integer>(){
      @Override
      public int compare(Integer i1, Integer i2){
        return i2 - i1;
      }
    });
    for(int x = 0; x < array.length; x++){
      if(x < k){
        maxHeap.offer(array[x]);
      }else if(array[x] < maxHeap.peek()){
        maxHeap.poll();
        maxHeap.offer(array[x]);
      }
    }
    int[] result = new int[k];
    for(int x = result.length - 1; x >= 0; x--){
      result[x] = maxHeap.poll();
    }
    return result;
  }
}
```
  
  
  The initialization of PriorityQueue can be implemented by lambda expression:
  ```
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(k , (i1, i2) -> (i2 - i1));
```

##### Compare Solution 1 & Solution 2
|   Type    |    Solution 1    | Solution 2 |
| ------ | ---------- | -------- |
| Average | O(N + KlogN) |  O(K + (N - k)logK)|
| N >>> K  | O(N)  | O(N * logK) |
| N = 2 * K|O(NlogN) | O(NlogN)
                                
                
#### Solution 3 : Quick Select  (**Offline Algorithm)**
  
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
    int index = partition(array, left, right);
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