## N Queens

#### Solution
DFS + check valid

    x
        x(x1, y1)         
            x       
                x(x0, y0)
                 

一个list 来存当前的Queens, target

```
case 1 : target == list.get(x) invalid
case 2 : Math.abs(y0 - y1) == x0 - x1 invalid
```

```java
public class Solution {
  public List<List<Integer>> nqueens(int n) {
		List<List<Integer>> result = new ArrayList<>();
		List<Integer> cur = new ArrayList<>();
		nqueensHelper(n, 0, result, cur);
		return result;
	  }
	
	  public void nqueensHelper(int n, int level, List<List<Integer>> result, List<Integer> cur){
		if(n == level){
		  result.add(new ArrayList<>(cur));
		  return;
		}
		for(int x = 0; x < n; x++){
		  if(checkValid(cur, x)){
			cur.add(x);
			nqueensHelper(n, level + 1, result, cur);
			cur.remove(cur.size() - 1);
		  }
		}
	  }
	
	  public boolean checkValid(List<Integer> cur, int target){
		int row = cur.size();
		for(int x = 0; x < row; x++){
			if(cur.get(x) == target || Math.abs(target - cur.get(x) == row - x){
				return false;
			}
		}
		return true;
	  }
}

```

