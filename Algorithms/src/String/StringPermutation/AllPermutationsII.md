## All Permutations II

Given a string with possible duplicate characters, return a list with all permutations of the characters.

* Examples

Set = “abc”, all permutations are [“abc”, “acb”, “bac”, “bca”, “cab”, “cba”]
Set = "aba", all permutations are ["aab", "aba", "baa"]
Set = "", all permutations are [""]
Set = null, all permutations are []

因为每层只确定当前层的字母是啥, 所以每一层可以使用一个set来判断是否重复

Time : N!

Space: N ^ 2

Code:
```java
public class Solution {
  public List<String> permutations(String set) {
    List<String> result = new ArrayList<>();
    if(set == null){
      return null;
    }else if(set.length() == 0){
      result.add("");
      return result;
    }
    char[] arr = set.toCharArray();
    permutationsHelper(result, arr, 0);
    return result;
  }

  public void permutationsHelper(List<String> result, char[] arr, int level){
    if(level == arr.length){
      result.add(new String(arr));
      return;
    }
    Set<Character> hashSet = new HashSet<>();
    for(int x = level; x < arr.length; x++){
      if(hashSet.add(arr[x])){
        swap(arr, x, level);
        permutationsHelper(result, arr, level + 1);
        swap(arr, x, level);
      }
    }
  }
  public void swap(char[] arr, int left, int right){
    char temp = arr[left];
    arr[left] = arr[right];
    arr[right] = temp;
  }
}

```
