## Reverse LinkedList
Use both the Iterative way and recursive way to implement this problem.

Iterative Way:
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
  public ListNode reverse(ListNode head) {
    if(head == null){
    	return null;
    }
    ListNode pre = null;
    ListNode cur = head;
    while( cur != null ){
    	ListNode next = cur.next;
    	cur.next = pre;
    	pre = cur;
    	cur = next;
    }
    return pre;
  }
}
```

Recursive Way:
```java
public class Solution {
  public ListNode reverse(ListNode head) {
    if(head == null || head.next == null){
    	return head;
    }
    ListNode newHead = reverse(head.next);
    head.next.next = head;
    head.next = null;
    return newHead;
  }
}
```