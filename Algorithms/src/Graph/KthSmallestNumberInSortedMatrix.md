## Kth Smallest Number In Sorted Matrix

Use the idea of Dijkstra Best first Search

Each step move to the next smallest value, after k step we can find the k-smallest value in this matrix

Solution 1:

Time : KlogK

Space : K + N ^ 2


Code:
```java
public class Solution {
  public int kthSmallest(int[][] matrix, int k) {
    // Write your solution here
    PriorityQueue<Element> minHeap = new PriorityQueue<>(new Comparator<Element>(){
      @Override
      public int compare(Element e1, Element e2){
        if(e1.val == e2.val){
          return 0;
        }
        return e1.val < e2.val ? -1 : 1; 
      }
    });
    boolean[][] visited = new boolean[matrix.length][matrix[0].length];
    minHeap.offer(new Element(0, 0, matrix[0][0]));
    for(int i = 0; i < k - 1; i++){
      Element cur = minHeap.poll();
      int x = cur.x;
      int y = cur.y;
      if(x < matrix.length - 1 && !visited[x + 1][y]){
        minHeap.offer(new Element(x + 1, y, matrix[x + 1][y]));
        visited[x + 1][y] = true;
      }
      if(y < matrix[0].length - 1 && !visited[x][y + 1]){
        minHeap.offer(new Element(x, y + 1, matrix[x][y + 1]));
        visited[x][y + 1] = true;
      }
    }
    return minHeap.peek().val;
  }

  class Element{
    int x;
    int y;
    int val;
    public Element(int x, int y, int val){
      this.x = x;
      this.y = y;
      this.val = val;
    }
  }
}

```

Solution 2:

We can we a HashSet instead of the boolean Matrix. So the time complexity can be optimized to O(K).
需要Override Element 类的equals 函数 和 hashCode函数

```java
public class Solution {
  public int kthSmallest(int[][] matrix, int k) {
    // Write your solution here
    PriorityQueue<Element> minHeap = new PriorityQueue<>(new Comparator<Element>(){
      @Override
      public int compare(Element e1, Element e2){
        if(e1.val == e2.val){
          return 0;
        }
        return e1.val < e2.val ? -1 : 1; 
      }
    });
    Set<Element> hashSet = new HashSet<>();
    minHeap.offer(new Element(0, 0, matrix[0][0]));
    for(int i = 0; i < k - 1; i++){
      Element cur = minHeap.poll();
      int x = cur.x;
      int y = cur.y;
      if(x < matrix.length - 1){
        Element e = new Element(x + 1, y, matrix[x + 1][y]);
        if(!hashSet.contains(e)){
          minHeap.offer(e);
          hashSet.add(e);
        }
      }
      if(y < matrix[0].length - 1){
        Element e = new Element(x, y + 1, matrix[x][y + 1]);
        if(!hashSet.contains(e)){
          minHeap.offer(e);
          hashSet.add(e);
        }
      }
    }
    return minHeap.peek().val;
  }

  class Element{
    int x;
    int y;
    int val;
    public Element(int x, int y, int val){
      this.x = x;
      this.y = y;
      this.val = val;
    }
    @Override
    public boolean equals(Object obj){
      if(obj == this){
        return true;
      }
      if(!(obj instanceof Element)){
        return false;
      }
      Element e = (Element)obj;
      return this.x == e.x && this.y == e.y;
    }

    @Override
    public int hashCode(){
      return 31 * x + y;
    }

  }
}

```