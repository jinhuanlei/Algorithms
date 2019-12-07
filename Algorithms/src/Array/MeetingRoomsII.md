## Meeting Rooms II

Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), find the minimum number of conference rooms required.

Example 1:

```
Input: [[0, 30],[5, 10],[15, 20]]
Output: 2
```
Example 2:
```
Input: [[7,10],[2,4]]
Output: 1
```
NOTE: input types have been changed on April 15, 2019. Please reset to default code definition to get new method signature.

```java
class Solution {
    public int minMeetingRooms(int[][] intervals) {
        if(intervals.length <= 0){
            return 0;
        }
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        Arrays.sort(intervals, (o1, o2) -> o1[0] - o2[0]);
        minHeap.add(intervals[0][1]);
        for(int x = 1; x < intervals.length; x++){
            if(!minHeap.isEmpty() && intervals[x][0] >= minHeap.peek()){
                minHeap.poll();
            }
            minHeap.offer(intervals[x][1]);
        }
        return minHeap.size();
    }
}
```