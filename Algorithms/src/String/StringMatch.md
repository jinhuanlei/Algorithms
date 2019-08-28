## String Match

### 1. Naive Solution O(N * M) 
N  : len(LongString)

M : len(Pattern)


### 2. Rabin-Karp fingerprinting algorithm

hash tips:
1. (10 * 65536 + 1) % 65521 === (10 * (65536 % 65521) + 1) % 65521 === 
((10 * 65536) % 65521 + 1) % 65521 === 151


### 3.  KMP