# LeetCode349. 两个数组的交集
**
给定两个数组，编写一个函数来计算它们的交集。
示例 1：
输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2]
示例 2：
输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[9,4]
说明：
输出结果中的每个元素一定是唯一的。
我们可以不考虑输出结果的顺序。
**
两个数组都转换为集合，然后迭代较小的集合，检查其中的每个元素是否同样存在于较大的集合中。
```
int* intersection(int* nums1, int nums1Size, int* nums2, int nums2Size, int* returnSize){
    int min=nums1Size<nums2Size?nums1Size:nums2Size;
    int* num=(int*)malloc(sizeof(int)*min);
    int cnt=0;
    for(int i=0;i<nums1Size;i++)
    {
        for(int j=0;j<nums2Size;j++)
        {
            if(nums1[i]==nums2[j])
            {
                int flag=0;
                for(int k=0;k<min;k++)
                {
                    if(num[k]==nums1[i])
                    flag=1;
                }
                if(flag!=1)
                {
                    num[cnt++]=nums1[i];
                }
                
            }
        }
    }
    *returnSize=cnt;
    return num;
}
```