# LeetCode1337. 方阵中战斗力最弱的 K 行
**
给你一个大小为 m * n的方阵 mat，方阵由若干军人和平民组成，分别用 1 和 0 表示。
请你返回方阵中战斗力最弱的 k 行的索引，按从最弱到最强排序。
如果第 i 行的军人数量少于第 j 行，或者两行军人数量相同但 i 小于 j，那么我们认为第 i 行的战斗力比第 j 行弱。
军人 总是 排在一行中的靠前位置，也就是说 1 总是出现在 0 之前。
例 1
输入：mat = 
[[1,1,0,0,0],
 [1,1,1,1,0],
 [1,0,0,0,0],
 [1,1,0,0,0],
 [1,1,1,1,1]], 
k = 3
输出：[2,0,3]
解释：
每行中的军人数目：
行 0 -> 2 
行 1 -> 4 
行 2 -> 1 
行 3 -> 2 
行 4 -> 5 
从最弱到最强对这些行排序后得到 [2,0,3,1,4]
示例 2：
输入：mat = 
[[1,0,0,0],
 [1,1,1,1],
 [1,0,0,0],
 [1,0,0,0]], 
k = 2
输出：[0,2]
解释： 
每行中的军人数目：
行 0 -> 1 
行 1 -> 4 
行 2 -> 1 
行 3 -> 1 
从最弱到最强对这些行排序后得到 [0,2,3,1]
提示：
m == mat.length
n == mat[i].length
2 <= n, m <= 100
1 <= k <= m
matrix[i][j] 不是 0 就是 1
**

官方解法：我们计算出方阵中每一行的战斗力（即每一行的元素之和），再对它们进行排序即可。较优的排序方式有两种：
待排序的列表中的每个元素包括行号和该行的战斗力。在排序时，我们可以直接按照战斗力为第一关键字，行号为第二关键字进行排序，需要用到的数据都存储在列表内；

```
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int count_number(int *arr,int arrSize){
    int count=0;
    for (int i=0;i<arrSize;i++){
        if (arr[i]==1)
            count++;
        else
            break;
    }
    return count;
}
int comp(const void *a,const void *b){
    return *(int*)a - *(int*)b;
}

int* kWeakestRows(int** mat, int matSize, int* matColSize, int k, int* returnSize){
    int *soldiers;
    *returnSize = k;
    soldiers = (int*)malloc(sizeof(int)*matSize);
    for (int i=0;i<matSize;i++){
        soldiers[i] = count_number(mat[i],matColSize[i])*matSize + i;
    }
    qsort(soldiers,matSize,sizeof(int),comp);
    for (int i=0;i<matSize;i++){
        soldiers[i] = soldiers[i]%matSize;
    }
    return soldiers;
}

```