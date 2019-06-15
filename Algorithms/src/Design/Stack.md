## Implement a Stack
Maintain a head.

每次添加元素, 都添加在head上, 每次删除也在head上删除.

## Using a Linked List

offer : O(1)

poll : O(1)

缺点是有额外的overhead, 空间开销会变大

Code :

```java

class LinkedStack {
    // implemented by LinkedList
    ListNode head;

    public LinkedStack() {
        head = null;
    }

    public void push(int x) {
        if (head == null) {
            head = new ListNode(x);
            return;
        }
        ListNode newHead = new ListNode(x);
        newHead.next = head;
        head = newHead;
    }

    public Integer pop() {
        if (head == null) {
            return null;
        }
        ListNode result = head;
        head = head.next;
        result.next = null;
        return result.val;
    }

    public Integer peek() {
        if (head == null) {
            return null;
        }
        return head.val;
    }

    public static void main(String[] args) {
        LinkedStack stack = new LinkedStack();
        System.out.println(stack.peek());
        stack.push(1);
        stack.push(4);
        stack.push(3);
        System.out.println(stack.peek());
        System.out.println(stack.pop());
        System.out.println(stack.pop());
        System.out.println(stack.pop());
        System.out.println(stack.pop());

    }
}
```

## Using a Array

offer : O(1) Worst O(N)

假入数组满了, 重新创建一个1.5倍大的数组. 

poll : O(1)

Time analysis : (N + 1 + 1 + 1 ... + 1)  / (0.5 * N) = 1.5N / 0.5N = 3 = O(1)

```java
class MyIntegerStack {
    int[] stack;
    int head;
    int size;
    public MyIntegerStack(){
        stack = new int[1];
        head = -1;
        size = 0;
    }

    public void push(Integer num){
        if(head == stack.length - 1){
            int newSize = (int)Math.ceil(stack.length * 1.5);
            int[] newStack = new int[newSize];
            for(int x = 0; x < stack.length; x++){
                newStack[x] = stack[x];
            }
            stack = newStack;
        }
        size++;
        stack[++head] = num;
    }

    public Integer pop(){
        if(head == -1){
            return null;
        }
        size--;
        return stack[head--];
    }

    public Integer peek(){
        if(head == -1){
            return null;
        }
        return stack[head];
    }

    public boolean empty(){
        return size == 0;
    }

    public int size(){
        return size;
    }
    
}
```