# LeetCode210. 课程表 II
**
现在你总共有 n 门课需要选，记为 0 到 n-1。
在选修某些课程之前需要一些先修课程。 例如，想要学习课程 0 ，你需要先完成课程 1 ，我们用一个匹配来表示他们: [0,1]
给定课程总量以及它们的先决条件，返回你为了学完所有课程所安排的学习顺序。
可能会有多个正确的顺序，你只要返回一种就可以了。如果不可能完成所有课程，返回一个空数组。
示例 1:
输入: 2, [[1,0]] 
输出: [0,1]
解释: 总共有 2 门课程。要学习课程 1，你需要先完成课程 0。因此，正确的课程顺序为 [0,1] 。
示例 2:
输入: 4, [[1,0],[2,0],[3,1],[3,2]]
输出: [0,1,2,3] or [0,2,1,3]
解释: 总共有 4 门课程。要学习课程 3，你应该先完成课程 1 和课程 2。并且课程 1 和课程 2 都应该排在课程 0 之后。
     因此，一个正确的课程顺序是 [0,1,2,3] 。另一个正确的排序是 [0,2,1,3] 。
说明:
输入的先决条件是由边缘列表表示的图形，而不是邻接矩阵。详情请参见图的表示法。
你可以假定输入的先决条件中没有重复的边。
提示:
这个问题相当于查找一个循环是否存在于有向图中。如果存在循环，则不存在拓扑排序，因此不可能选取所有课程进行学习。
通过 DFS 进行拓扑排序 - 一个关于Coursera的精彩视频教程（21分钟），介绍拓扑排序的基本概念。
拓扑排序也可以通过 BFS 完成。
**
跟上题几乎一样的思路
```
int** edges;
int* edgeColSize;
int* visited;
int* result;
int resultSize;
bool valid;

void dfs(int u) {
    visited[u] = 1;
    for (int i = 0; i < edgeColSize[u]; ++i) {
        if (visited[edges[u][i]] == 0) {
            dfs(edges[u][i]);
            if (!valid) {
                return;
            }
        } else if (visited[edges[u][i]] == 1) {
            valid = false;
            return;
        }
    }
    visited[u] = 2;
    result[resultSize++] = u;
}

int* findOrder(int numCourses, int** prerequisites, int prerequisitesSize, int* prerequisitesColSize, int* returnSize) {
    valid = true;
    edges = (int**)malloc(sizeof(int*) * numCourses);
    for (int i = 0; i < numCourses; i++) {
        edges[i] = (int*)malloc(0);
    }
    edgeColSize = (int*)malloc(sizeof(int) * numCourses);
    memset(edgeColSize, 0, sizeof(int) * numCourses);
    visited = (int*)malloc(sizeof(int) * numCourses);
    memset(visited, 0, sizeof(int) * numCourses);
    for (int i = 0; i < prerequisitesSize; ++i) {
        int a = prerequisites[i][1], b = prerequisites[i][0];
        edgeColSize[a]++;
        edges[a] = (int*)realloc(edges[a], sizeof(int) * edgeColSize[a]);
        edges[a][edgeColSize[a] - 1] = b;
    }
    result = (int*)malloc(sizeof(int) * numCourses);
    resultSize = 0;
    for (int i = 0; i < numCourses && valid; ++i) {
        if (!visited[i]) {
            dfs(i);
        }
    }
    for (int i = 0; i < numCourses; i++) {
        free(edges[i]);
    }
    free(edges);
    free(edgeColSize);
    free(visited);
    if (!valid) {
        *returnSize = 0;
    } else
        *returnSize = numCourses;
    for (int i = 0; i < numCourses / 2; i++) {
        int t = result[i];
        result[i] = result[numCourses - i - 1], result[numCourses - i - 1] = t;
    }
    return result;
}


```