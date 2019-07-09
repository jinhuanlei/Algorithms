## Reverse Nodes in k-Group
Given a linked list, reverse the nodes of a linked list k at a time and return its modified list. If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is. You may not alter the values in the nodes, only nodes itself may be changed.

#### Example

Given this linked list: 1->2->3->4->5

For k = 2, you should return: 2->1->4->3->5

For k = 3, you should return: 3->2->1->4->5

#### Code
```java
/**
 * class ListNode {
 *   public int value;
 *   public ListNode next;
 *   public ListNode(int value) {
 *     this.value = value;
 *     next = null;
 *   }
 * }
 */
public class Solution {
  public ListNode reverseKGroup(ListNode head, int k) {
    if(head == null){
      return head;
    }
    int num = k;
    ListNode pre = null;
    ListNode cur = head;
    while(num > 0){
      if(cur == null){
        return head;
      }
      pre = cur;
      cur = cur.next;
      num--;
    }
    ListNode nextHead = reverseKGroup(cur, k);
    ListNode iter = head;
    ListNode preIter = null;
    while(iter != cur){
      ListNode next = iter.next;
      iter.next = preIter;
      preIter = iter;
      iter = next;
    }
    head.next = nextHead;
    return pre;
  }
}

```
 