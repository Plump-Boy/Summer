# LeetCode18.四数之和
**
给定一个包含 n 个整数的数组 nums 和一个目标值 target，判断 nums 中是否存在四个元素 a，b，c 和 d ，使得 a + b + c + d 的值与 target 相等？找出所有满足条件且不重复的四元组。
注意：
答案中不可以包含重复的四元组。
示例：
给定数组 nums = [1, 0, -1, 0, -2, 2]，和 target = 0。
满足要求的四元组集合为：
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
**
快排，动态申请指针数据空间，保存返回数据数组指针，循环调用三数之和函数（上一题函数），最后去重
```
int comp(const void *a, const void *b)
{
    return *(int *)a - *(int *)b;
}

int threeSum(int* nums, int numsSize, int target, int **pRetPoint)
{
    int     i       = 0;
    int     iLeft   = 0;
    int     iRight  = numsSize - 1;
    int     iBak_0  = -99;
    int     iBak_1  = -99;
    int     iBak_2  = -99;
    int     iRetSize = 0;
    int     iTmpSum = 0;



    for (i = 1; i < numsSize - 1; i++)
    {

        if (nums[i] != nums[i - 1])
        {
            iLeft = 0;
            iRight = numsSize - 1;
        }

        while ((iLeft < i) && (iRight > i))
        {


            iTmpSum = nums[iLeft] + nums[i] + nums[iRight];


            if ((nums[iLeft] + nums[i] + nums[iRight]) < target)
            {
              
                iLeft += 1;
            }
            else if ((nums[iLeft] + nums[i] + nums[iRight]) > target)
            {
                
                iRight -= 1;
            }
            else 
            {
               
                if (!((iBak_0 == nums[iLeft]) && (iBak_1 == nums[i]) && (iBak_2 == nums[iRight])))
                {
                    
                    pRetPoint[iRetSize] = malloc(sizeof(int) * 4);
                    pRetPoint[iRetSize][0] = nums[iLeft];
                    pRetPoint[iRetSize][1] = nums[i];
                    pRetPoint[iRetSize][2] = nums[iRight];
                    
                    iRetSize += 1;

                    iBak_0 = nums[iLeft];
                    iBak_1 = nums[i];
                    iBak_2 = nums[iRight];                  
                }

                iLeft += 1;
            }
        }
    }

    return iRetSize;
}

int removeRepeat(int **pRetPoint, int retSize)
{
    int     i           = 0;
    int     j           = 0;
    int     iRetSize    = retSize;

    for (i = 0; i < iRetSize - 1; i++)
    {
        for (j = i + 1; j < iRetSize; j++)
        {
            if ((pRetPoint[i][0] == pRetPoint[j][0]) &&
                (pRetPoint[i][1] == pRetPoint[j][1]) &&
                (pRetPoint[i][2] == pRetPoint[j][2]) &&
                (pRetPoint[i][3] == pRetPoint[j][3]))
            {
            
                free(pRetPoint[j]);
                memmove(&pRetPoint[j], &pRetPoint[j + 1], sizeof(char *) * (iRetSize - j - 1));
                iRetSize -= 1;
                j -= 1;
            }
        }
    }
    return iRetSize;
}

int** fourSum(int* nums, int numsSize, int target, int* returnSize, int** returnColumnSizes){
    int     **ppRet     = NULL;
    int     i           = 0;
    int     j           = 0;
    int     iRet        = 0;
    int     iRetSize    = 0;

  
    qsort(nums, numsSize, sizeof(int), comp);

    ppRet = (int **)malloc(sizeof(int *) * (numsSize + 1) * 6);
    *returnColumnSizes = malloc(sizeof(int) * (numsSize + 1) * 6);

  
    for (i = numsSize - 1; i >= 3; i--)
    {
        iRet = threeSum(nums, i, target - nums[i], &ppRet[iRetSize]);



        if (iRet > 0)
        {
            for (j = 0; j < iRet; j++)
            {
                ppRet[iRetSize + j][3] = nums[i];
                (*returnColumnSizes)[iRetSize + j] = 4;
            }
        }
        iRetSize += iRet;
    }


    iRetSize = removeRepeat(ppRet, iRetSize);

    *returnSize = iRetSize;
    return ppRet;
}
```