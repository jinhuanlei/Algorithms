## Char Deduplication Adjacent Letters Repeatedly
#### Solution 1 : with a Stack




#### Solution 2 : Use a pointer **(in place)**
Case 1 : [slow - 1] != [fast]
  
  1. [slow++] = [fast++]
  
Case 2 : [slow - 1] == [fast]

1. traverse util not repeat

1. slow--
       



```java
public class Solution {
  public String deDup(String input) {
    if(input == null || input.length() <= 1){
      return input;
    }
    char[] arr = input.toCharArray();
    int slow = 1;
    int fast = 1;
    while(fast < input.length()){
      if(slow == 0 || arr[slow - 1] != arr[fast]){
        arr[slow++] = arr[fast++];
      }else{
        while(fast < input.length() && arr[slow - 1] == arr[fast]){
          fast++;
        }
        slow--;
      }
    }
    return new String(arr, 0, slow);
  }
}
```