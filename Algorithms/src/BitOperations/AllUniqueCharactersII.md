## All Unique Characters II

Determine if the characters of a given string are all unique.

#### Assumptions

We are using ASCII charset, the value of valid characters are from 0 to 255
The given string is not null

#### Examples

all the characters in "abA+\8" are unique

"abA+\a88" contains duplicate characters

a - z 可以用26位的数字来表示是否存在
ASCII 有256位, 可以用8个32位的Integer来表示


code
```java
public class Solution {
  public boolean allUnique(String word) {
    int[] arr = new int[256 / 32];
    for(int x = 0; x < word.length(); x++){
      int val = (int)word.charAt(x);
      int row = val / 32;
      int col = val % 32;
      if(((arr[row] >> col) & 1) == 1){
        return false;
      }else{
        arr[row] |= (1 << col);
      }
    }
    return true;
  }
}
```