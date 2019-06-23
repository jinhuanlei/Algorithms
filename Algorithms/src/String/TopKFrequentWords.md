## Top K Frequent Words
Same questions just as smallest k elements.

As we discussed before, we can use Min heap to implement this.

* Step1: Use a HashMap to count Strings   O(N)

* Step2: Build a MinHeap with size of k   O(K)

* Step3: traverse entry set of hashMap    O((N - k)logK)

Time: O(K + (N - k)logK)
```java
public class Solution {
  public String[] topKFrequent(String[] combo, int k) {
    // Write your solution here
    Map<String, Integer> hm = new HashMap<>();
    for(String str : combo){
      hm.put(str, hm.getOrDefault(str, 0) + 1);
    }
    PriorityQueue<Map.Entry<String, Integer>> pq = new PriorityQueue<>(new Comparator<Map.Entry<String, Integer>>(){
      @Override
      public int compare(Map.Entry<String, Integer> e1, Map.Entry<String, Integer> e2){
        if(e1.getValue() == e2.getValue()){
          return 0;
        }
        return e1.getValue() < e2.getValue() ? -1 : 1;
      }
    });
    for(Map.Entry<String, Integer> entry : hm.entrySet()){
      if(pq.size() < k){
        pq.offer(entry);
      }else if(pq.size() == k && entry.getValue() > pq.peek().getValue()){
        pq.poll();
        pq.offer(entry);
      }
    }
    String[] result = new String[pq.size()];
    int index = result.length - 1;
    while(!pq.isEmpty()){
      result[index--] = pq.poll().getKey();
    }
    return result;
  }
}

```
