## 3 Sum
Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

#### Note:
The solution set must not contain duplicate triplets.

#### Example:
    Given array nums = [-1, 0, 1, 2, -1, -4],
    
    A solution set is:
    [
      [-1, 0, 1],
      [-1, -1, 2]
    ]
    
#### Analysis
通过固定一个值, 然后通过双指针相向而行来找到相反值的two sum

Time : NlogN + N ^ 2 = N ^ 2

Space : if MergeSort N   if  QuickSort logN
#### Code
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        if(nums == null || nums.length == 0){
            return new ArrayList<List<Integer>>();
        }
        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList<>();
        for(int x = 0; x < nums.length - 2; x++){
            if(x == 0 || (x >= 1 && nums[x] != nums[x - 1])){
                threeSumHelper(result, x, nums);
            }
        }
        return result;
    }
    
    public void threeSumHelper(List<List<Integer>> result, int index, int[] nums){
        int left = index + 1;
        int right = nums.length - 1;
        int target = -nums[index];
        while(left < right){
            if(nums[left] + nums[right] == target){
                List<Integer> cur = new ArrayList<>();
                cur.add(nums[index]);
                cur.add(nums[left]);
                cur.add(nums[right]);
                result.add(cur);
                left++;
                right--;
                while(left < right && nums[left] == nums[left - 1]){
                    left++;
                }
                while(left < right && nums[right + 1] == nums[right]){
                    right--;
                }
            }else if(nums[left] + nums[right] < target){
                left++;
            }else{
                right--;
            }
        }
    }
}
```