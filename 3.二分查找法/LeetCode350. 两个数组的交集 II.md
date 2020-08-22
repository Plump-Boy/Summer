# LeetCode350. 两个数组的交集 II
**
给定两个数组，编写一个函数来计算它们的交集。
示例 1：
输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2,2]
示例 2:
输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[4,9]
说明：
输出结果中每个元素出现的次数，应与元素在两个数组中出现次数的最小值一致。
我们可以不考虑输出结果的顺序。
**
对两个数组进行排序，然后使用两个指针遍历两个数组。比较其数字，如果不相等则小数字指针右移，相等则把数字添加到答案
```
int COMP(const void *a, const void *b)
{
    return (*(int *)a > *(int *)b);
}
#define MIN(a, b) ((a) < (b) ? (a) : (b))

int *my_func(int *s_num, int s_size, int *l_num, int l_size, int *ret_size)
{
    int *ret = (int *)calloc(s_size, sizeof(int));
    int i = 0;
    int j = 0;
    int idx = 0;
    while (i < s_size && j < l_size) {
        if (s_num[i] == l_num[j]) {
            ret[idx++] = s_num[i];
            i++;
            j++;
        } else if (s_num[i] < l_num[j]) {
            i++;
        } else { // s_num[i] > l_num[j]
            j++;
        }
    }
    *ret_size = idx;
    return ret;
}

int* intersect(int* nums1, int nums1Size, int* nums2, int nums2Size, int* returnSize){
    *returnSize = 0;
    if (nums1 == NULL || nums2 == NULL || nums1Size == 0 || nums2Size == 0) {
        return NULL;
    }

    qsort(nums1, nums1Size, sizeof(int), COMP);
    qsort(nums2, nums2Size, sizeof(int), COMP);

    int *ret;
    if (nums1Size < nums2Size) {
        ret = my_func(nums1, nums1Size, nums2, nums2Size, returnSize);
    } else {
        ret = my_func(nums2, nums2Size, nums1, nums1Size, returnSize);
    }
    return ret;
}
```