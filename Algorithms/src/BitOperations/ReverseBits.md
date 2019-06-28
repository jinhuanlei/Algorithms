## Reverse Bits

Solution 1

code:
```java
public class Solution {
  public long reverseBits(long n) {
    long result = 0;
    for(int x = 0; x < 32; x++){
      long cur = n & 1;
      result <<= 1;
      result += cur;
      n >>>= 1;
    }
    return result;
  }
}
```

Solution 2

code:
```java
public class Solution {
  public long reverseBits(long n) {
    long left = 0;
    long right = 31;
    while(left < right){
      n = swap(n, left++, right--);
    }
    return n;
  }

  public long swap(long n, long left, long right){
    long lBit = ((n >> left) & 1);
    long rBit = ((n >> right) & 1);
    if(lBit != rBit){
      n ^= ((Long.valueOf(1) << left) | (Long.valueOf(1) << right));
    }
    return n;
  }
}
```