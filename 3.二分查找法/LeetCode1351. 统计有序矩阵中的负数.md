# LeetCode1351. 统计有序矩阵中的负数
**
给你一个 m * n 的矩阵 grid，矩阵中的元素无论是按行还是按列，都以非递增顺序排列。 
请你统计并返回 grid 中 负数 的数目。
示例 1：
输入：grid = [[4,3,2,-1],[3,2,1,-1],[1,1,-1,-2],[-1,-1,-2,-3]]
输出：8
解释：矩阵中共有 8 个负数。
示例 2：
输入：grid = [[3,2],[1,0]]
输出：0
示例 3：
输入：grid = [[1,-1],[-1,-1]]
输出：3
示例 4：
输入：grid = [[-1]]
输出：1
提示：
m == grid.length
n == grid[i].length
1 <= m, n <= 100
-100 <= grid[i][j] <= 100
**

注意到题目中给了一个性质，即矩阵中的元素无论是按行还是按列，都以非递增顺序排列，可以考虑把这个性质利用起来优化暴力。已知这个性质告诉了我们每一行的数都是有序的，所以我们通过二分查找可以找到每一行中从前往后的第一个负数，那么这个位置之后到这一行的末尾里所有的数必然是负数了，可以直接统计。

```
int countNegatives(int** grid, int gridSize, int* gridColSize){
    int x = 0;
    int num = 0;
    for(int i=0;i<gridSize;i++){
        int j = 0;
        int count = 0;
        while(j<*gridColSize && grid[i][j]>=0){
            count++;
            j++;
        }
        num+=(*gridColSize-count);
    }
    return num;
}

```