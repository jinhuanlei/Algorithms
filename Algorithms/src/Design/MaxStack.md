## Design a Max Stack
**Amazon Onsite questions**

Solution 1: (Deprecated)
* Using a Max Heap to find out the max node

* Using a Linked List to simulate the stack activities

我本来以为已知节点删除可以 O(1), 但是要改变另一个node里的值, 会破坏priorityqueue的结构.
而且没有考虑到重复元素返回的插入顺序是什么, 下次不要直接做题 要clarification!!!!!!!!!!!!!!!!
    


Solution 2:

Three stacks

Code:

```java
class MaxStack {

    /** initialize your data structure here. */
    Deque<Integer> stack;
    Deque<Integer> maxStack;
    Deque<Integer> buffer;
    public MaxStack() {
        stack = new ArrayDeque<>();
        maxStack = new ArrayDeque<>();
        buffer = new ArrayDeque<>();
    }
    
    public void push(int x) {
        stack.offerFirst(x);
        if(maxStack.isEmpty()){
            maxStack.offerFirst(x);
        }else{
            maxStack.offerFirst(maxStack.peekFirst() > x ? maxStack.peekFirst() : x);
        }
    }
    
    public int pop() {
        maxStack.pollFirst();
        return stack.pollFirst();
    }
    
    public int top() {
        return stack.peekFirst();
    }
    
    public int peekMax() {
        return maxStack.peekFirst();
    }
    
    public int popMax() {
        int result = maxStack.peekFirst();
        if(stack.peekFirst() == maxStack.peekFirst()){
            return pop();
        }else{
            while(!stack.isEmpty()){
                int val1 = stack.pollFirst();
                int val2 = maxStack.pollFirst();
                if(val1 == val2){
                    break;
                }
                buffer.offerFirst(val1);
            }
            while(!buffer.isEmpty()){
                push(buffer.pollFirst());
            }
        }
        return result;
    }
}

/**
 * Your MaxStack object will be instantiated and called as such:
 * MaxStack obj = new MaxStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.peekMax();
 * int param_5 = obj.popMax();
 */
```