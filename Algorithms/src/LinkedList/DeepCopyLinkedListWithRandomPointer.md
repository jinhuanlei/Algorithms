## Deep Copy Linked List With Random Pointer
Each of the nodes in the linked list has another pointer pointing to a random node in the list or null. 
Make a deep copy of the original list.

#### Idea
需要有一个Map去记录一个映射关系， 把老节点和新节点的映射关系给记住

#### Code
```java
/**
 * class RandomListNode {
 *   public int value;
 *   public RandomListNode next;
 *   public RandomListNode random;
 *   public RandomListNode(int value) {
 *     this.value = value;
 *   }
 * }
 */
public class Solution {
  public RandomListNode copy(RandomListNode head) {
    if(head == null){
      return head;
    }
    RandomListNode dummyHead = new RandomListNode(0);
    Map<RandomListNode,RandomListNode> hm = new HashMap<>();
    // copy List
    RandomListNode cur1 = dummyHead;
    // origin List
    RandomListNode cur2 = head;
    while(cur2 != null){
      RandomListNode newNode = new RandomListNode(cur2.value);
      hm.put(cur2, newNode);
      cur1.next = newNode;
      cur1 = cur1.next;
      cur2 = cur2.next;
    }
    cur1 = dummyHead.next;
    cur2 = head;
    while(cur2 != null){
      RandomListNode rand = cur2.random;
      if(hm.containsKey(rand)){
        cur1.random = hm.get(rand);
      }
      cur1 = cur1.next;
      cur2 = cur2.next;
    }
    return dummyHead.next;
  }
}
```