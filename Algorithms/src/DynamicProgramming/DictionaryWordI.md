## Dictionary Word I
Given a word and a dictionary, determine if it can be composed by concatenating words from the given dictionary.

#### Assumptions

The given word is not null and is not empty
The given dictionary is not null and is not empty and all the words in the dictionary are not null or empty

#### Examples

Dictionary: {“bob”, “cat”, “rob”}

Word: “robob” return false

Word: “robcatbob” return true since it can be composed by "rob", "cat", "bob"

#### Analysis
左大段右小段的思想，所谓大段，就是说我不需要再重新计算，而是通过读表格的方式，
直接读出 M[i] 的值而得到Solution.所谓小段，就是我们不读 M[i] 表格，
而是直接 manual 操作（通过题目已知条件直接得出）

(N represents the length of the String)

Time:N ^ 2 * N(contains may cause N to calculate the hashcode) ==> N ^ 3

Space: N

Code:
```java
public class Solution {
  public boolean canBreak(String input, String[] dict) {
    Set<String> hs = toSet(dict);
    boolean[] memory = new boolean[input.length() + 1];
    memory[0] = true;
    for(int x = 1; x <= input.length(); x++){
    	for(int y = 0; y < x; y++){
    		if(memory[y] && hs.contains(input.substring(y, x))){
    			memory[x] = true;
    			break;
    		}
    	}
    }
    return memory[input.length()];
  }

  public Set<String> toSet(String[] dict){
  	Set<String> hs = new HashSet<>();
  	for(String str : dict){
  		hs.add(str);
  	}
  	return hs;
  }
}

```