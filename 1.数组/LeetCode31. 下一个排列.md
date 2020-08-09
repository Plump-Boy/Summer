# LeetCode31. 下一个排列
**
实现获取下一个排列的函数，算法需要将给定数字序列重新排列成字典序中下一个更大的排列。
如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）。
必须原地修改，只允许使用额外常数空间。
以下是一些例子，输入位于左侧列，其相应输出位于右侧列。
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
**
从后往前遍历，建立一个滑窗，滑窗从头到尾为降序，头指向第一个破坏降序的数字，尾部指向后面比该数字大的数字，交换数字位置
```
static int comp(const void* a, const void* b)
{
    return *(int*)a - *(int*)b;
}

void nextPermutation(int* nums, int numsSize){
    if (NULL == nums || 0 == numsSize)
    {
        return;
    } 

    int left = numsSize - 2; 
    int right = 0;
    int temp = 0;

    while (left >= 0)
    {
        if (nums[left] < nums[left + 1]) 
        {
            break;
        }

        left--;
    }

    if (-1 == left) 
    {   
        return qsort(nums, numsSize, sizeof(int), comp);
    }

    for (right = left + 1; right <= numsSize - 1 && nums[left] < nums[right]; right++)
    {
        NULL;
    }

    temp = nums[left];
    nums[left] = nums[right - 1];
    nums[right - 1] = temp;

    qsort(nums + left + 1, numsSize - 1 - left, sizeof(int), comp);
}
```