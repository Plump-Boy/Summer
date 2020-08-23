# LeetCode310. 最小高度树
**
对于一个具有树特征的无向图，我们可选择任何一个节点作为根。图因此可以成为树，在所有可能的树中，具有最小高度的树被称为最小高度树。给出这样的一个图，写出一个函数找到所有的最小高度树并返回他们的根节点。
格式
该图包含 n 个节点，标记为 0 到 n - 1。给定数字 n 和一个无向边 edges 列表（每一个边都是一对标签）。
你可以假设没有重复的边会出现在 edges 中。由于所有的边都是无向边， [0, 1]和 [1, 0] 是相同的，因此不会同时出现在 edges 里。
示例 1:
输入: n = 4, edges = [[1, 0], [1, 2], [1, 3]]
        0
        |
        1
       / \
      2   3 
输出: [1]
示例 2:
输入: n = 6, edges = [[0, 3], [1, 3], [2, 3], [4, 3], [5, 4]]
     0  1  2
      \ | /
        3
        |
        4
        |
        5 
输出: [3, 4]
说明:
 根据树的定义，树是一个无向图，其中任何两个顶点只通过一条路径连接。 换句话说，一个任何没有简单环路的连通图都是一棵树。
树的高度是指根节点和叶子节点之间最长向下路径上边的数量。
**
参考自LeetCode题解：矩阵或链式存储图，利用节点的度概念，每层遍历删除度为1的节点，注意删除度为1的节点时，需要判断这个节点所在边的对端节点的度不为1，如果对端为1，这不能删除，这是这两个节点均为有效解，该题解个个数范围，可能是1个，可能是2个。
```
int* findMinHeightTrees(int n, int** edges, int edgesSize, int* edgesColSize, int* returnSize){
    short *map = malloc(sizeof(short) * n * n);
    int *retEdges = malloc(sizeof(int) * n);
    char *flag = malloc(sizeof(char) * n);
    char *tmpflag = malloc(sizeof(char) * n);
    short *alldu = malloc(sizeof(short) * n);
    short *tmpalldu = malloc(sizeof(short) * n);
    int bcontinue = 1;
    int du = 0;
    int index = 0;
    memset(map, 0 , sizeof(short) * n * n);
    memset(flag, 0 , sizeof(char) * n);
    memset(tmpflag, 0 , sizeof(char) * n);
    memset(alldu, 0 , sizeof(short) * n);
    memset(tmpalldu, 0 , sizeof(short) * n);
    
    for (int i = 0; i < edgesSize; ++i) {
        map[edges[i][0] * n + edges[i][1]] = 1;
        map[edges[i][1] * n + edges[i][0]] = 1;
        alldu[edges[i][0]]++;
        alldu[edges[i][1]]++;
    }
    memcpy(tmpalldu, alldu, sizeof(short) * n);
    while (bcontinue) {
        bcontinue = 0;
        for (int i = 0; i < n; ++i) {
            if (flag[i] == 1 || alldu[i] != 1)
                continue;
            du = 0;
            for (int j = 0; j < n; ++j) {
                if (flag[j] == 1)
                    continue;
                if (map[i * n + j] == 1) {
                    index = j;
                    break;
                }
            }
            
            if (alldu[index] != 1) {
                tmpflag[i] = 1;
                tmpalldu[index]--;
                bcontinue = 1;
            }
        }
        memcpy(flag, tmpflag, sizeof(char) * n);
        memcpy(alldu, tmpalldu, sizeof(short) * n);
    }
    
    *returnSize = 0;
    for (int i = 0; i < n; ++i) {
        if(flag[i] == 0) {
            retEdges[*returnSize] = i;
            *returnSize += 1;
        }
    }

    return retEdges;
}


```