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
        int len = copyDigitsToArray(arr, slow, count);
        slow += len;
      }
    }
    return slow - 1;
  }

// 尽量避免使用String.valueOf() 因为具有时空复杂度 
// 原来我写的是 String.valueOf(count); 然后结合charAt()来拷贝元素, 老师说这有logN的空间复杂度
  public int copyDigitsToArray(char[] arr, int index, int count){
    int len = 0;
    for(int x = count; x > 0; x /= 10){
      len++;
      index++;
    }
    while(count > 0){
      arr[--index] = (char)('0' + count % 10);
      count /= 10;
    }
    return len;
  }

  public int getNewLength(char[] arr, int index){
    // calculate new length
    int newLength = index + 1;
    for(int x = 0; x <= index; x++){
      if(Character.isLetter(arr[x]) && (x == index || Character.isLetter(arr[x + 1]))){
        newLength += 1;
      }
    }
    return newLength;
  }

  public String encodeLongPattern(char[] arr, int index){
    int newLength = getNewLength(arr, index);
    char[] result = new char[newLength];
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