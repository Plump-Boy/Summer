# LeetCode1042. 不邻接植花
**
有 N 个花园，按从 1 到 N 标记。在每个花园中，你打算种下四种花之一。
paths[i] = [x, y] 描述了花园 x 到花园 y 的双向路径。
另外，没有花园有 3 条以上的路径可以进入或者离开。
你需要为每个花园选择一种花，使得通过路径相连的任何两个花园中的花的种类互不相同。
以数组形式返回选择的方案作为答案 answer，其中 answer[i] 为在第 (i+1) 个花园中种植的花的种类。花的种类用  1, 2, 3, 4 表示。保证存在答案。
示例 1：
输入：N = 3, paths = [[1,2],[2,3],[3,1]]
输出：[1,2,3]
示例 2：
输入：N = 4, paths = [[1,2],[3,4]]
输出：[1,2,1,2]
示例 3：
输入：N = 4, paths = [[1,2],[2,3],[3,4],[4,1],[1,3],[2,4]]
输出：[1,2,3,4]
提示：
1 <= N <= 10000
0 <= paths.size <= 20000
不存在花园有 4 条或者更多路径可以进入或离开。
保证存在答案。
**
参考LeetCode上面的解法：1，构图。
利用无向图的邻接表表示法，将花园和路径输入。此时任意一个花园的状态都是未种花的，且处于能种任意一种花的状态。

2，种花。
遍历花园：
如果某个花园没有同其他花园相连，则可以任意种任意一种花；
如果某个花园同其他花园有连接，则遍历其允许种花的状态，将第一个允许种的花种上。然后再遍历与其相连的花园，将这些花园中允许种该花的可能去除掉。

3，返回每个花园所种花的种类。

```
#define MAXVEX 10000
#define MAXTYPE 4
//定义顶点数据类型
typedef int VertexType;
//定义邻接表
typedef struct EdgeNode{
    int adjvex;
    struct EdgeNode *next;
}EdgeNode;
//定义顶点结构
typedef struct VertexNode{
    VertexType data;
    int type;//定义花的种类。0表示还未种花，其他正整数表示已经种花。
    int status[MAXTYPE];//定义允许种的花，0表示允许，1表示禁止。
    EdgeNode *firstedge;
}VertexNode, AdjList[MAXVEX];
//定义图
typedef struct{
    AdjList adjList;
    int numVertexes, numEdges;
}GraphAdjList;
//图的生成
GraphAdjList * CreateALGraph(int N, int** paths, int pathsSize, int* pathsColSize);
//打印节点和边的信息
void Print(GraphAdjList * G);
//种花
void Plant(GraphAdjList *G);

int* gardenNoAdj(int N, int** paths, int pathsSize, int* pathsColSize, int* returnSize){
    GraphAdjList * G = CreateALGraph(N, paths, pathsSize, pathsColSize);
    //Print(G);
    Plant(G);
    int * ans = malloc(sizeof(int)*N);
    for(int i=0; i<N; i++)
        ans[i] = G->adjList[i].type;
    *returnSize = N;
    return ans;
}
//生成图
GraphAdjList * CreateALGraph(int N, int** paths, int pathsSize, int* pathsColSize){
    int i, j, k;
    EdgeNode *e;
    GraphAdjList * G = malloc(sizeof(GraphAdjList));
    G->numVertexes = N;
    G->numEdges = pathsSize;
    for(i=0; i<G->numVertexes; i++){
        G->adjList[i].data = i+1;
        G->adjList[i].type = 0;//0表示花还未种。
        for(j=0; j<MAXTYPE; j++)
            G->adjList[i].status[j] = 0;//0表示允许中的花，1表示禁止中的花。
        G->adjList[i].firstedge = NULL;
    }
    for(k=0; k<G->numEdges; k++){
        i = paths[k][0];
        j = paths[k][1];
        //正向
        e = (EdgeNode *)malloc(sizeof(EdgeNode));
        e->adjvex = j;
        e->next = G->adjList[i-1].firstedge;
        G->adjList[i-1].firstedge = e;
        //反向
        e = (EdgeNode *)malloc(sizeof(EdgeNode));
        e->adjvex = i;
        e->next = G->adjList[j-1].firstedge;
        G->adjList[j-1].firstedge = e;
    }
    return G;
}
//打印图中顶点和边的信息
void Print(GraphAdjList * G){
    int i;
    for(i=0; i<G->numVertexes; i++){
        if(G->adjList[i].firstedge == NULL)
            printf("%d\n", G->adjList[i].data);
        else{
            printf("%d->", G->adjList[i].data);
            EdgeNode * p = G->adjList[i].firstedge;
            while(p != NULL){
                if(p->next != NULL)
                    printf("%d->", p->adjvex);
                else
                    printf("%d\n", p->adjvex);
                p = p->next;
            }
        }
    }
}
//种花
void Plant(GraphAdjList *G){
    int i,j;
    for(i=0; i<G->numVertexes; i++){
        if(G->adjList[i].firstedge == NULL)//如果没有邻接表，则随意种花。
            G->adjList[i].type = 1;
        else{
            //如果没有种花，则种能种的花。
            if(G->adjList[i].type == 0)
                for(j=0; j<MAXTYPE; j++)
                    if(G->adjList[i].status[j] == 0){
                        G->adjList[i].type = j+1;
                        break;
                    }
            //去除与该节点花园有关系的花园中种该花的可能性。
            EdgeNode * p = G->adjList[i].firstedge;
            while(p != NULL){
                if(G->adjList[p->adjvex-1].type == 0)
                    G->adjList[p->adjvex-1].status[G->adjList[i].type-1] = 1;
                p = p->next;
            }
        }
    }
}
```