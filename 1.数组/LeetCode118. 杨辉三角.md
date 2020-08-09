# LeetCode118. 杨辉三角
**
给定一个非负整数 numRows，生成杨辉三角的前 numRows 行。
在杨辉三角中，每个数是它左上方和右上方的数的和。
示例:
输入: 5
输出:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
**
每层第一个和最后一个是1，其他是左上与右上的和
```
int** generate(int numRows, int* returnSize, int** returnColumnSizes){
    *returnSize=numRows;
    *returnColumnSizes=(int*)malloc(4*numRows);
    int i,j;
    int**ret=(int**)malloc(sizeof(int*)*numRows);
    for(i=0;i<numRows;++i)
    {
        (*returnColumnSizes)[i]=i+1;
        ret[i]=(int*)malloc(i*4+4);
        ret[i][0]=1;
        ret[i][i]=1;
    }
    for(i=2;i<numRows;++i)
        for(j=1;j<i;++j)
            ret[i][j]=ret[i-1][j-1]+ret[i-1][j];
    return ret;
}

```