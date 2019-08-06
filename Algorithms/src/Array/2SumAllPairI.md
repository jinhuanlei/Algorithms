## 2 Sum All Pair I
Find all pairs of elements in a given array that sum to the given target number. Return all the pairs of indices.

#### Assumptions

The given array is not null and has length of at least 2.

#### Examples

A = {1, 3, 2, 4}, target = 5, return [[0, 3], [1, 2]]

A = {1, 2, 2, 4}, target = 6, return [[1, 3], [2, 3]]

#### Solution
很秀的方法， dedup
Time : N (worst N ^ 2)
Space : N
```java
public class Solution {
  public List<List<Integer>> allPairs(int[] array, int target) {
    List<List<Integer>> result = new ArrayList<>();
    Map<Integer, List<Integer>> hm = new HashMap<>();
    for(int x = 0; x < array.length; x++){
    	List<Integer> indeces = hm.get(target - array[x]);
    	if(indeces != null){
    		for(int i : indeces){
    			result.add(Arrays.asList(x, i));
    		}
    	}
    	if(!hm.containsKey(array[x])){
    		hm.put(array[x], new ArrayList<Integer>());
    	}
      hm.get(array[x]).add(x);
    }
    return result;
  }
}

```