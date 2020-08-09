# LeetCode119. 杨辉三角 II
**
给定一个非负索引 k，其中 k ≤ 33，返回杨辉三角的第 k 行。
在杨辉三角中，每个数是它左上方和右上方的数的和。
示例:
输入: 3
输出: [1,3,3,1]
**
用递归算法，一行一行求解
```
int* getRow(int rowIndex, int* returnSize){
    int *res = (int *)calloc(10000, sizeof(int));
    if(rowIndex == 0)
    {
        *returnSize = 1;
        res[0] = 1;
        return res;
    }
    int size = rowIndex;
    *returnSize = size;
    int *lastRow = getRow(rowIndex - 1, returnSize);
    int i;
    
    for(i = 0;i <= rowIndex;i++)
    {
        if(i == 0 || i == rowIndex)
        {
            res[i] = 1;
        }
        else
        {
            res[i] = lastRow[i - 1] + lastRow[i];
        }
    }
    *returnSize = i;
    return res;
    
}
```