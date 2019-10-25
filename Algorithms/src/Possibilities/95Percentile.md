## 95 Percentile
Given a list of integers representing the lengths of urls, find the 95 percentile of all lengths (95% of the urls have lengths <= returned length).

#### Assumptions

The maximum length of valid url is 4096

The list is not null and is not empty and does not contain null

#### Examples

[1, 2, 3, ..., 95, 96, 97, 98, 99, 100], 95 percentile of all lengths
 is 95.
 
#### Solution

solution 1

sort + index
Time : NlogN
Space : logN or N(according to the algorithms)
```java
public class Solution {
  public int percentile95(List<Integer> lengths) {
    Collections.sort(lengths);
    int index = (int)Math.ceil(lengths.size() * 0.95) - 1;
    return lengths.get(index);
  }
}
```

solution 2

bucket sort
Time : N
Space : 1
```java
public class Solution {
  public int percentile95(List<Integer> lengths) {
    int[] bucket = new int[4097];
    for(int x : lengths){
      bucket[x] += 1;
    }
    int len = 4097;
    int num = 0;
    while(num <= lengths.size() * 0.05){
      num += bucket[--len];
    }
    return len;
  }
}

```