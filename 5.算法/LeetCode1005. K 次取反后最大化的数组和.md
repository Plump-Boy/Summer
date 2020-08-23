# LeetCode1005. K 次取反后最大化的数组和
**
给定一个整数数组 A，我们只能用以下方法修改该数组：我们选择某个索引 i 并将 A[i] 替换为 -A[i]，然后总共重复这个过程 K 次。（我们可以多次选择同一个索引 i。）
以这种方式修改数组后，返回数组可能的最大和。
示例 1：
输入：A = [4,2,3], K = 1
输出：5
解释：选择索引 (1,) ，然后 A 变为 [4,-2,3]。
示例 2：
输入：A = [3,-1,0,2], K = 3
输出：6
解释：选择索引 (1, 2, 2) ，然后 A 变为 [3,1,0,2]。
示例 3：
输入：A = [2,-3,-1,5,-4], K = 2
输出：13
解释：选择索引 (1, 4) ，然后 A 变为 [2,3,-1,5,4]。
提示：
1 <= A.length <= 10000
1 <= K <= 10000
-100 <= A[i] <= 100
**
把其中的负数序列与非负数分开，根据k的值不同情况来取值
```
int cmp(const void *a, const void *b) {
    return *(int*)a - *(int*)b;
}

int largestSumAfterKNegations(int* A, int ASize, int K){
    qsort(A, ASize, sizeof(int), cmp);
    int l=0,r=ASize-1;
    while (l <= r) {
        int center = (l+r)/2;
        if (A[center] < 0) {
            l = center + 1; // l means numbers of negative
        } else {
            r = center - 1;
        }
    }
    int sum = 0;
    for (int i=l; i<ASize; ++i) sum += A[i];
    for (int i=0; i<l; ++i) {
        if (K > 0) {
            --K;
            sum -= A[i];
        } else {
            sum += A[i];
        }
    }
    K %= 2;
    if (K == 1) {
        if (l > 0 && -A[l-1] < A[l]) sum += 2*A[l-1];
        else 
            sum -= 2*A[l];
    }

    return sum;
}
```