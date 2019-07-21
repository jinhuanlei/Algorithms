## Largest And Second Largest(Least Comparison)
Use the least number of comparisons to get the largest and 2nd largest number in the given integer array. Return the largest number and 2nd largest number.

#### Assumptions

The given array is not null and has length of at least 2
#### Examples

{2, 1, 5, 4, 3}, the largest number is 5 and 2nd largest number is 4.

#### Idea
compare and swap, 每次只换大的那一半， n / 2 + 4 / n + ... + 1 = N

每次把比较过的值存在List里， 然后花费logN的次数来找到second Largest

Total comparison  N + logN

#### Code
```java
public class Solution {
	static class Element{
		int val;
		List<Integer> comparedValues;
		public Element(int val){
			this.val = val;
			comparedValues = new ArrayList<>();
		}
	}

  public int[] largestAndSecond(int[] array) {
    Element[] elements =  convert(array);
    int len = array.length;
    while(len > 1){
    	compareAndSwap(elements, len);
    	// 保证奇数的时候能多算一个, 偶数保持不变
    	len = (len + 1) / 2;
    }
    return new int[]{elements[0].val, largest(elements[0].comparedValues)};
  }

  public int largest(List<Integer> list){
  	int max = list.get(0);
  	for(int x = 1; x < list.size(); x++){
  		max = Math.max(max, list.get(x));
  	}
  	return max;
  }

  public void compareAndSwap(Element[] arr, int len){
  	for(int x = 0; x < len / 2; x++){
  		if(arr[x].val < arr[len - 1 - x].val){
  			swap(arr, x, len - 1 - x);
  		}
  		arr[x].comparedValues.add(arr[len - 1 - x].val);
  	}
  }

  public void swap(Element[] arr, int x, int y){
    Element temp  = arr[x];
    arr[x] = arr[y];
    arr[y] = temp;
  }

  public Element[] convert(int[] array){
  	Element[] result = new Element[array.length];
  	for(int x = 0; x < array.length; x++){
  		result[x] = new Element(array[x]);
  	}
  	return result;
  }
}

```