## Remove Certain Characters

slow, fast双指针, 同向而行

* [0, s) the character we want to keep
* [s, f) we don't care
* [f, len - 1] ready to process

Time : N

Space: 1


Code:
```java
public class Solution {
  public String remove(String input, String t) {
    if(t == null || t.length() == 0 || input.length() == 0){
      return input;
    }
    Set<Character> hashSet = new HashSet<>();
    for(int x = 0; x < t.length(); x++){
      hashSet.add(t.charAt(x));
    }
    char[] arr = input.toCharArray();
    int slow = 0;
    for(int fast = 0; fast < arr.length; fast++){
      if(!hashSet.contains(arr[fast])){
        arr[slow++] = arr[fast];
      }
    }
    return new String(arr, 0, slow);
  }
}
```