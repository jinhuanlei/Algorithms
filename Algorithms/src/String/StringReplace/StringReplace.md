## String Replace

Solution 1 : Using String API
Time: O(N)
Space: O(N)
```java
public class Solution {
  public String replace(String input, String source, String target) {
    StringBuilder sb = new StringBuilder();
    int fromIndex = 0;
    int matchIndex = input.indexOf(source);
    while(matchIndex != -1){
      sb.append(input, fromIndex, matchIndex).append(target);
      fromIndex = matchIndex + source.length();
      matchIndex = input.indexOf(source, fromIndex);
    }
    sb.append(input, fromIndex, input.length());
    return new String(sb);
  }
}

```

Solution 2 : In-place with two pointer
Case 1 : long word => short word

simple two pointer solution

Case 2 : short word => long word

Step 1 : find all occurrence of source words

Step 2 : expand the array

Step 3 : use two pointer from right to left


```java
public class Solution {
  public String replace(String input, String source, String target) {
    if(source.length() >= target.length()){
      // long words => short word
      return replaceShoterWord(input, source, target);
    }else{
      return replaceLongerWord(input, source, target);
    } 
  }

  public String replaceLongerWord(String input, String source, String target){
    // find all the occurrance of substring first
    List<Integer> occurrance = new ArrayList<>();
    int index = input.indexOf(source);
    while(index != -1){
      occurrance.add(index + source.length() - 1);
      index = input.indexOf(source, index + source.length());
    }
    // append spaces in the tail
    char[] arr = new char[input.length() + occurrance.size() * (target.length() - source.length())];
    int fast = input.length() - 1;
    int slow = arr.length - 1;
    int lastIndex = occurrance.size() - 1;
    while(fast >= 0){
      if(lastIndex >= 0 && fast == occurrance.get(lastIndex)){
        copyArr(arr, slow, target);
        slow -= target.length();
        fast -= source.length();
        lastIndex--;
      }else{
        arr[slow--] = input.charAt(fast--);
      }
    }
    return new String(arr);
  }

  public void copyArr(char[] arr, int index, String target){
    for(int x = target.length() - 1; x >= 0; x--){
      arr[index--] = target.charAt(x);
    }
  }

  public String replaceShoterWord(String input, String source, String target){
    int slow = 0;
    int fast = 0;
    char[] arr = input.toCharArray();
    while(fast < arr.length){
      if(arr[fast] == source.charAt(0) && isMatch(arr, fast, source)){
        for(int x = 0; x < target.length(); x++){
          arr[slow++] = target.charAt(x);
        }
        fast += source.length();
      }else{
        arr[slow++] = arr[fast++];
      }
    }
    return new String(arr, 0, slow);
  }

  public boolean isMatch(char[] arr, int index, String source){
    if(index > arr.length - source.length()){
      return false;
    }
    for(int x = 0; x < source.length(); x++){
      if(arr[x + index] != source.charAt(x)){
        return false;
      }
    }
    return true;
  }
}

```

