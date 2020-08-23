# LeetCode1029. 两地调度
**
公司计划面试 2N 人。第 i 人飞往 A 市的费用为 costs[i][0]，飞往 B 市的费用为 costs[i][1]。
返回将每个人都飞到某座城市的最低费用，要求每个城市都有 N 人抵达。
示例：
输入：[[10,20],[30,200],[400,50],[30,20]]
输出：110
解释：
第一个人去 A 市，费用为 10。
第二个人去 A 市，费用为 30。
第三个人去 B 市，费用为 50。
第四个人去 B 市，费用为 20。
最低总费用为 10 + 30 + 50 + 20 = 110，每个城市都有一半的人在面试。
**
参考题解：先默认所有人飞到A城市，再将飞到A城市和飞到B城市的差价进行排序，选出最小的一般人，改为飞到B城市。
```
typedef struct _price{
    int priceA;
    int priceB;
    int priceDiff;
}price;

int cmp(const void *a, const void *b){
    price* A = (price*)a;
    price* B = (price*)b;
    return A->priceDiff - B->priceDiff;
}

int twoCitySchedCost(int** costs, int costsSize, int* costsColSize){
    price* P = (price*)malloc(costsSize * sizeof(price));
    int sum = 0;
    for(int i = 0; i < costsSize; i++){
        P[i].priceA = costs[i][0];  
        P[i].priceB = costs[i][1];  
        P[i].priceDiff = costs[i][1] - costs[i][0]; 
        sum += costs[i][0];        
    }
    qsort(P, costsSize, sizeof(price), cmp);    
    for(int i = 0; i < costsSize / 2; i++)
        sum += P[i].priceDiff;                 
    
    return sum;
}

```