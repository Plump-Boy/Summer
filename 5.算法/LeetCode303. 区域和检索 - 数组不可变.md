# LeetCode303. 区域和检索 - 数组不可变
**
给定一个整数数组  nums，求出数组从索引 i 到 j  (i ≤ j) 范围内元素的总和，包含 i,  j 两点。
示例：
给定 nums = [-2, 0, 3, -5, 2, -1]，求和函数为 sumRange()
sumRange(0, 2) -> 1
sumRange(2, 5) -> -1
sumRange(0, 5) -> -3
说明:
你可以假设数组不可变。
会多次调用 sumRange 方法。
**
暴力法，每次都用for将元素相加
```
typedef struct {
    int *nums;
} NumArray;

int *Sums;

NumArray* numArrayCreate(int* nums, int numsSize) {
    int i;
    NumArray* temp = malloc(sizeof(NumArray));
    temp->nums = nums;

    if(numsSize <= 0)
        return;
    Sums = (int *)malloc(sizeof(int ) * numsSize);
    Sums[0] = nums[0];
    for(i = 1; i < numsSize; i++)
        Sums[i] = Sums[i - 1] + nums[i];

    return temp;
}

int numArraySumRange(NumArray* obj, int i, int j) {
    if(i == 0)
        return Sums[j];
    else
        return Sums[j] - Sums[i - 1];
}

void numArrayFree(NumArray* obj) {
    if(obj != NULL)
    {
        free(obj);
        obj = NULL;
    }
}
```