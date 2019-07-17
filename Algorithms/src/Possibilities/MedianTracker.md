## Median Tracker
Given an unlimited flow of numbers, keep track of the median of all elements seen so far.

You will have to implement the following two methods for the class

* read(int value) - read one value from the flow
* median() - return the median at any time, return null if there is no value read so far
#### Examples

read(1), median is 1

read(2), median is 1.5

read(3), median is 2

read(10), median is 2.5

......

#### Idea
maintain两个Heap， 左边的是maxheap右边的是minheap， 每次添加完element要保证
size(left) == size(right) or size(left) == size(right + 1)

#### Code
```java
public class Solution {
  PriorityQueue<Integer> left;
  PriorityQueue<Integer> right;
  public Solution() {
    left = new PriorityQueue(Collections.reverseOrder());
    right = new PriorityQueue();
  }
  
  public void read(int value) {
    if(left.size() == 0 && right.size() == 0){
      left.offer(value);
      return;
    }
    if(value > left.peek()){
    	right.offer(value);
    	if(left.size() < right.size()){
    		left.offer(right.poll());
    	}
    }else{
      left.offer(value);
    	if(left.size() > right.size() + 1){
    		right.offer(left.poll());
    	}
    }
  }
  
  public Double median() {
    if(left.size() == 0 && right.size() == 0){
      return null;
    }
    if(left.size() == right.size()){
    	return (double)(left.peek() + right.peek()) / 2;
    }
    return Double.valueOf(left.peek());
  }
}

```