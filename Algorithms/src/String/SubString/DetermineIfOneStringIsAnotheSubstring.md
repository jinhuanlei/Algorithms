## Determine If One String Is Another's Substring
Solution 1 : Easy version of Rabin-Karp

没有考虑hash溢出的情况

Large with len1

Small with len2

average Time : (len1 + len2) worst(len1 * len2)

space O(1)

Code:
```java
public class Solution {
  public int strstr(String large, String small) {
    if(small.length() == 0){
      return 0;
    }
    int target = hash(small);
    int curHash = 0;
    for(int x = 0; x < large.length(); x++){
      curHash += large.charAt(x);
      if(x >= small.length()){
        curHash -= large.charAt(x - small.length());
      }
      if(x >= small.length() - 1){
        if(curHash == target && compare(large, small, x - small.length() + 1, x)){
          return x - small.length() + 1;
        }
      }
    }
    return -1;
  }

  public boolean compare(String large, String small, int left, int right){
    int index = 0;
    for(int x = left; x <= right; x++){
      if(large.charAt(x) != small.charAt(index++)){
        return false;
      }
    }
    return true;
  }

  public int hash(String str){
    int result = 0;
    for(int x = 0; x < str.length(); x++){
      result += str.charAt(x);
    }
    return result;
  }
}

```