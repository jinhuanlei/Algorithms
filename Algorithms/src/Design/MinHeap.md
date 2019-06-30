## Min Heap

Code:
```java
public class Heap{
    // Min Heap
    int[] heap;
    int size;
    private static final double RESIZE_SCALE = 1.5;
    public Heap(int[] array){
        heap = new int[array.length];
        for(int x = 0; x < array.length; x++){
            heap[x] = array[x];
        }
        size = array.length;
        heapify();
    }

    public boolean isEmpty(){
        return size == 0;
    }

    public int size(){
        return size;
    }

    public Integer peek(){
        if(size == 0){
            return null;
        }
        return heap[0];
    }

    public Integer poll(){
        if(size == 0){
            return null;
        }
        int result = heap[0];
        heap[0] = heap[size - 1];
        size--;
        percolateDown(0);
        return result;
    }

    public void offer(int val){
        if(size == heap.length){
            int[] newHeap = new int[(int)(heap.length * RESIZE_SCALE)];
            for(int x = 0; x < heap.length; x++){
                newHeap[0] = heap[0];
            }
            heap = newHeap;
        }
        heap[size++] = val;
        percolateUp(size - 1);
    }

    public void percolateUp(int index){
        while(index > 0){
            int parent = (index - 1) / 2;
            if(heap[index] < heap[parent]){
                swap(index, parent);
                index = parent;
            }else{
                return;
            }
        }
    }

    public void percolateDown(int index){
        // last index is size - 1
        // ((size - 1) - 1) / 2 
        // 这是最后一个node的parent
        while(index <= size / 2 - 1){
            int left = index * 2 + 1;
            int right = index * 2 + 2;
            int swapCandidate = left;
            if(right < size && heap[right] < heap[left]){
                swapCandidate = right;
            }
            if(heap[index] > heap[swapCandidate]){
                swap(index, swapCandidate);
                index = swapCandidate;
            }else{
                return;
            }
        }
    }

    public void heapify(){
        for(int x = size / 2 - 1; x >= 0; x--){
            percolateDown(x);
        }
    }

    public void swap(int x, int y){
        int temp = heap[x];
        heap[x] = heap[y];
        heap[y] = temp;
    }
    public static void main(String[] args) {
        int[] testArr = new int[]{4,7,8,5,1,66,7,3,5,9};
        Heap h = new Heap(testArr);
        while(!h.isEmpty()){
            // System.out.println("Peek:" + h.peek());
            System.out.println("Poll:" + h.poll());
        }
    }
}
```