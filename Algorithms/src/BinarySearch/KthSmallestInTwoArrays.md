## K-th Smallest In Two Sorted Arrays

### Solution 1 
谁小移谁

Time = O(K) if K is two large O(len(arr1) + len(arr2))

### Solution 2
把A[N] 和 B[M] 的各前k/2的元素比较， 每次删除k/2 ， 比较A[N] 和 B[M] 谁小删谁
**反证法: Easy to prove**

Arr1: xxxxxxxxxxxxxKxxxXxxxxxxxxxxxxxxxx

Arr2: yyyyyyyyyyyyyyyyyYyyyyyyyyyyyyyyyy

如果X小于Y，则第k小的值肯定不在X的左边。 如果在假设在K处

len1 ： K < index of X

len2 : < index of Y **because X < Y and K < X**

len1 + len2 = k / 2 - 1 + k / 2 - 1 = K - 2 != k 与一直条件冲突

**Time: O(logK)**

```java
public class Solution {
  public int kth(int[] a, int[] b, int k) {
    // Write your solution here
    return kthHelper(a, b, 0, 0, k);
  }

  public int kthHelper(int[] a, int[] b, int aLeft, int bLeft, int k){
    // base case
    if(aLeft >= a.length){
      return b[bLeft + k - 1];
    }
    if(bLeft >= b.length){
      return a[aLeft + k - 1];
    }
    if(k == 1){
      return Math.min(a[aLeft], b[bLeft]);
    }
    // consider k is not index so we need to do k / 2 - 1
    int curALeft = aLeft + k / 2 - 1;
    int curBLeft = bLeft + k / 2 - 1;
    int valA = curALeft < a.length ? a[curALeft] : Integer.MAX_VALUE;
    int valB = curBLeft < b.length ? b[curBLeft] : Integer.MAX_VALUE;
    if(valA < valB){
      return kthHelper(a, b, curALeft + 1, bLeft, k - k / 2);
    }else{
      return kthHelper(a, b, aLeft, curBLeft + 1, k - k / 2);
    }
  }
}

```