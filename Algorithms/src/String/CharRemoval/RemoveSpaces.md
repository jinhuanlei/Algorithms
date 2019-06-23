## Remove Spaces
Given a string, remove all leading/trailing/duplicated empty spaces.

Assumptions:
* The given string is not null.

Examples:

* “  a” --> “a”
* “   I     love MTV ” --> “I love MTV”

Case 1 : [fast] != ' '  ->   [slow++] = [fast++]

Case 2 [fast] == ' '

  Case 2.1 slow == 0  ->   fast++
  
  Case 2.2 [slow] == ' ' -> fast++
  
  Case 2.3 [slow] != ' ' -> [slow++] = [fast++]
  
  Code:
  ```java
public class Solution {
  public String removeSpaces(String input) {
    char[] arr = input.toCharArray();
    int slow = 0;
    int fast = 0;
    while(fast < arr.length){
      if(arr[fast] != ' '){
        arr[slow++] = arr[fast++];
      }else if(slow == 0 || arr[slow - 1] == ' '){
        fast++;
      }else if(arr[slow - 1] != ' '){
        arr[slow++] = arr[fast++]; 
      }
    }
    // post processing
    if(slow > 0 && arr[slow - 1] == ' '){
      slow--;
    }
    return new String(arr, 0, slow);
  }
}

```
  
