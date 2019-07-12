##Container With Most Water
Given n non-negative integers a1, a2, ..., an , where each represents a point 
at coordinate (i, ai). n vertical lines are drawn such that the two endpoints
 of line i is at (i, ai) and (i, 0). Find two lines, which together with 
 x-axis forms a container, such that the container contains the most water.

![avatar](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

Note: You may not slant the container and n is at least 2.

#### Analysis:
双指针相向而行, 谁小移谁
#### Code:
```java
class Solution {
    public int maxArea(int[] height) {
        int globalMax = 0;
        int left = 0;
        int right = height.length - 1;
        while(left < right){
            int contains = (right - left) * Math.min(height[right], height[left]);
            globalMax = Math.max(globalMax, contains);
            if(height[right] > height[left]){
                left++;
            }else{
                right--;
            }
        }
        return globalMax;
    }
}
```
