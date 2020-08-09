# LeetCode167. 两数之和 II - 输入有序数组
**
给定一个已按照升序排列 的有序数组，找到两个数使得它们相加之和等于目标数。
函数应该返回这两个下标值 index1 和 index2，其中 index1 必须小于 index2。
说明:
返回的下标值（index1 和 index2）不是从零开始的。
你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。
示例:
输入: numbers = [2, 7, 11, 15], target = 9
输出: [1,2]
解释: 2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。
**
双指针初始化：左指针第0个元素，右指针第numsSize-1个元素，循环：如果相等存取index，返回；如果>target，右指针前移；如果<target，左指针后移
```
#define NUM_MAX 2
int g_arr[NUM_MAX];

int *twoSum(int *nums, int numsSize, int target, int *returnSize)
{
    int start = 0, end = numsSize - 1;

    memset(g_arr, 0, sizeof(int) * NUM_MAX);
    while (start < end) {
        if (nums[start] + nums[end] == target) {
            g_arr[0] = start + 1;
            g_arr[1] = end + 1;
            break;
        } else if (nums[start] + nums[end] > target) {
            end -= 1;
        } else if (nums[start] + nums[end] < target) {
            start += 1;
        }
    }

    *returnSize = NUM_MAX;
    return g_arr;
}
```