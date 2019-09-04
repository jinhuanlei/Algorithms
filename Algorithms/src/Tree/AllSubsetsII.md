## All Subsets II
Given a set of characters represented by a String, return a list containing all subsets of the characters. Notice that each subset returned will be sorted to remove the sequence.

#### Assumptions

There could be duplicate characters in the original set.

​#### Examples

Set = "abc", all the subsets are ["", "a", "ab", "abc", "ac", "b", "bc", "c"]

Set = "abb", all the subsets are ["", "a", "ab", "abb", "b", "bb"]

Set = "abab", all the subsets are ["", "a", "aa","aab", "aabb", "ab","abb","b", "bb"]

Set = "", all the subsets are [""]

Set = null, all the subsets are []

#### Solution
```java
public class Solution {
  public List<String> subSets(String set) {
    if(set == null){
      return new ArrayList<String>();
    }
    char[] arr = set.toCharArray();
    Arrays.sort(arr);
    StringBuilder sb = new StringBuilder();
    List<String> result = new ArrayList<>();
    subSetsHelper(arr, result, sb, 0);
    return result;
  }

  public void subSetsHelper(char[] arr, List<String> result, StringBuilder sb, int level){
    if(level == arr.length){
      result.add(new String(sb));
      return;
    }
    sb.append(arr[level]);
    subSetsHelper(arr, result, sb, level + 1);
    sb.deleteCharAt(sb.length() - 1);
    // 要么要要么都不要
    while(level < arr.length - 1 && arr[level] == arr[level + 1]){
      level++;
    }
    subSetsHelper(arr, result, sb, level + 1);
    }
  }
```