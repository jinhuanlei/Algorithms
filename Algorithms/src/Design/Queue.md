## Implement a Queue
       
**Data Structure with FIFO**
    
#### Use Linked List

Maintain a head and list two pointer. Insert at tail, remove at head.

* offer : O(1)

* poll : O(1)

Code:
```java
class LinkedQueue {
    // implemented by Linked List
    ListNode head;
    ListNode tail;

    public LinkedQueue() {
        head = null;
        tail = null;
    }

    public void offer(Integer x) {
        if(tail == null){
            tail = new ListNode(x);
            head = tail;
            return;
        }
        ListNode newNode = new ListNode(x);
        tail.next = newNode;
        tail = tail.next;
    }

    public Integer poll(){
        if(head == null){
            return null;
        }
        ListNode result = head;
        head = head.next;
        if(head == null){
            tail = null;
        }
        return result.val;
    }

    public Integer peek(){
        if(head == null){
            return null;
        }
        return head.val;
    }

    public static void main(String[] args) {
        LinkedQueue queue = new LinkedQueue();
        queue.offer(1);
        queue.offer(2);
        queue.offer(3);
        System.out.println(queue.peek());
        System.out.println(queue.poll());
        System.out.println(queue.poll());
        System.out.println(queue.poll());
        System.out.println(queue.poll());
        System.out.println(queue.peek());
    }
}
```

#### Use Array
Implement with array. We need to expand extra functions to extend the array because the size of the array is fixed.

* offer : O(1) worst O(N)

* poll : O(1)

Code:
```java
class ArrayQueue{
    int[] queue;
    int head;
    int tail;
    // (head, tail)
    // head == tail full
    // head + 1 == tail empty
    public ArrayQueue(){
        queue =  new int[2];
        head = 0;
        tail = 1;
    }

    public void offer(int val){
        if(head == tail){
            int[] newArr = new int[(int)Math.ceil(queue.length * 1.5)];
            for(int x = 0; x < queue.length; x++){
                newArr[x] = queue[x];
            }
            queue = newArr;
        }
        queue[tail] = val;
        tail = (tail + 1 == queue.length ? 0 : tail + 1);
    }

    public Integer poll(){
        if(head == tail - 1){
            return null;
        }
        head = (head + 1 == queue.length ? 0 : head + 1);
        return queue[head];
    }

    public Integer peek(){
        if(head == tail - 1){
            return null;
        }
        int index = (head + 1 == queue.length ? 0 : head + 1);
        return queue[index];
    }

    public static void main(String[] args) {
        ArrayQueue queue = new ArrayQueue();
        queue.peek();
        queue.offer(1);
        System.out.println(queue.poll());
        queue.offer(2);
        queue.offer(3);
        queue.offer(4);
        queue.offer(5);
        System.out.println(queue.peek());
        System.out.println(queue.poll());
        System.out.println(queue.peek());
        System.out.println(queue.poll());
        System.out.println(queue.poll());
        System.out.println(queue.poll());
        System.out.println(queue.poll());
        System.out.println(queue.poll());
        System.out.println(queue.poll());
    }
}
```






