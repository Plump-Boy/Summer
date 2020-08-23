# LeetCode055. 跳跃游戏
**
给定一个非负整数数组，你最初位于数组的第一个位置。
数组中的每个元素代表你在该位置可以跳跃的最大长度。
判断你是否能够到达最后一个位置
示例 1:
输入: [2,3,1,1,4]
输出: true
解释: 我们可以先跳 1 步，从位置 0 到达 位置 1, 然后再从位置 1 跳 3 步到达最后一个位置。
示例 2:
输入: [3,2,1,0,4]
输出: false
解释: 无论怎样，你总会到达索引为 3 的位置。但该位置的最大跳跃长度是 0 ， 所以你永远不可能到达最后一个位置。
**

```
bool canJump(int* nums, int numsSize){
    if (numsSize == 0) return false;
    int * maxjump_arr = (int *)malloc(sizeof(int) * numsSize);
    int max_jump = 0;
    memset(maxjump_arr, 0, sizeof(int) * numsSize);
    for (int i = 0; i < numsSize; i++) {
        maxjump_arr[i] = i + nums[i];
    }


    for (int i = 0; i < numsSize; i++) {
        if (maxjump_arr[i] > max_jump) {
            max_jump = maxjump_arr[i];
        }
        if(i >= max_jump){ 
            break;
        }
    }
    //printf("%d ", max_tmp);
    if (max_jump >= numsSize -1 ) return true;

    return false;
}
```