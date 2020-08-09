# LeetCode16. 最接近的三数之和
**
给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。
示例：
输入：nums = [-1,2,1,-4], target = 1
输出：2
解释：与 target 最接近的和是 2 (-1 + 2 + 1 = 2) 。
提示：
3 <= nums.length <= 10^3
-10^3 <= nums[i] <= 10^3
-10^4 <= target <= 10^4
**
leetcode上面的题解：先快速排序，再用双指针找三数之和用一个变量gap记录 sum和target的距离（即差的绝对值）, ret记录此时的返回值若有sum = target，直接返回sum。否则所有循环结束后返回ret
```
int comp(const void* a, const void* b) {
    return *(int*)a - *(int*)b;
}
int threeSumClosest(int* nums, int numsSize, int target) {
    int ret, gap = 0x7fffffff;  
    qsort(nums, numsSize, sizeof(int), comp);
    for (int i = 0; i < numsSize - 2; i++) {
        int left = i + 1;
        int right = numsSize - 1;
        while (left < right) {
            int sum = nums[i] + nums[left] + nums[right];
            if (abs(sum - target) < gap) {    
                gap = abs(sum - target);
                ret = sum;
            }
            if (sum > target) right--;      
            else if (sum < target) left++;
            else return sum;
        }
    }
    return ret;
}
```