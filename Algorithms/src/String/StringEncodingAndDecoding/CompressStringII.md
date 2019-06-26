Compress String II

Given a string, replace adjacent, repeated characters with the character followed by the number of repeated occurrences.

Assumptions

The string is not null

The characters used in the original string are guaranteed to be ‘a’ - ‘z’

Examples

“abbcccdeee” → “a1b2c3d1e3”


Step 1:
encode from “abbcccdeee” => 'ab2c3de3'

Step2:
encode from 'ab2c3de3' to “a1b2c3d1e3”

Code:
```java
public class Solution {
  public String compress(String input) {
    if(input.length() <= 1){
      return input;
    }
    char[] arr = input.toCharArray();
    return encodeLongPattern(arr, encodeShortPattern(arr));
  }

  public int encodeShortPattern(char[] arr){
    int slow = 1;
    int fast = 1;
    while(fast < arr.length){
      if(arr[fast] != arr[slow - 1]){
        arr[slow++] = arr[fast++];
      }else{
        int count = 1;
        while(fast < arr.length && arr[fast] == arr[slow - 1]){
          fast++;
          count++;
        }
        String str = String.valueOf(count);
        for(int x = 0; x < str.length(); x++){
          arr[slow++] = str.charAt(x);
        }
      }
    }
    return slow - 1;
  }

  public String encodeLongPattern(char[] arr, int index){
      // assume I can get enough spaces 我算了个预计最大值, 不是很inplace hahahaha
    char[] result = new char[(index + 1) * 2];
    int slow = 1;
    int fast = 1;
    result[0] = arr[0];
    while(fast <= index){
      if(Character.isDigit(arr[fast])){
        result[slow++] = arr[fast++];
      }else{
        if(Character.isDigit(result[slow - 1])){
          result[slow++] = arr[fast++];
        }else{
          result[slow++] = '1';
        }
      }
    }
    if(Character.isLetter(result[slow - 1])){
      result[slow++] = '1';
    }
    return new String(result, 0, slow);
  }
}

```