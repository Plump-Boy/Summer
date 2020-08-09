# LeetCode15. 三数之和

**
给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有满足条件且不重复的三元组。
注意：答案中不可以包含重复的三元组。
示例：
给定数组 nums = [-1, 0, 1, 2, -1, -4]，
满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
**
先排序；然后建立内外循环遍历，第一个数去重，条件是与外循环的前一个数对比，第二个数去重，条件是：当A+B+C = 0时，B与后一个数对比；第三个数去重，条件是：当A+B+C = 0时，C与后一个数对比
```
#define MAX_SIZE 100000

int cmp(const void *a, const void *b)
{
    return ( *(int *)a - *(int *)b );
}


int** threeSum(int* nums, int numsSize, int* returnSize, int** returnColumnSizes){
    int** res = (int **)calloc(MAX_SIZE,sizeof(int*));
    *returnColumnSizes = malloc(sizeof(int *) * MAX_SIZE);
    int i,L,R,sum;
    
    *returnSize = 0;
    qsort(nums, numsSize, sizeof(int), cmp);
    for(i = 0; i <= numsSize - 3;i++)
    {
        if(i > 0 && nums[i] == nums[i - 1])
            continue;
        #printf("%d\n",i);
        L = i + 1;
        R = numsSize - 1;
        while(R > L)
        {
            sum = nums[i] + nums[L] + nums[R];
            if(sum == 0)
            {
                res[*returnSize] = (int *)calloc(3,sizeof(int));
                (*returnColumnSizes)[*returnSize] = 3;
                
                res[*returnSize][0] = nums[i];
                res[*returnSize][1] = nums[L];
                res[*returnSize][2] = nums[R];
                (*returnSize)++;
                L++;
                R--;
                while(nums[L] == nums[L-1] && L < R)
                    L++;
                while(nums[R] == nums[R+1] && L < R)
                    R--;
            }
            else if(sum < 0)
            {
                L++;
            }
            else
            {
                R--;
            }
        }
    }
    
    
    return res;
}
```