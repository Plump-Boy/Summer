# LeetCode1122. 数组的相对排序

**
给你两个数组，arr1 和 arr2，
arr2 中的元素各不相同
arr2 中的每个元素都出现在 arr1 中
对 arr1 中的元素进行排序，使 arr1 中项的相对顺序和 arr2 中的相对顺序相同。未在 arr2 中出现过的元素需要按照升序放在 arr1 的末尾。
示例：
输入：arr1 = [2,3,1,3,2,4,6,7,9,2,19], arr2 = [2,1,4,3,9,6]
输出：[2,2,2,1,4,3,3,9,6,7,19]
提示：
arr1.length, arr2.length <= 1000
0 <= arr1[i], arr2[i] <= 1000
arr2 中的元素 arr2[i] 各不相同
arr2 中的每个元素 arr2[i] 都出现在 arr1 中
**
与递增递减排序不同，本题是根据数组顺序自定义排序，因此最适合计数排序来实现（桶排序）
因为题意说明数组中元素在0~1000之间，因此定义一个容量为1000的桶
第一个循环对数组1中的元素进行计数，结果保存在桶中
第二个循环通过数组2，将重合的元素从数组1的0位置开始插入
第三个循环，搜索桶中剩余的数组1元素，并把它们插入到数组1的后面。

```
int cmp(const void *a, const void *b) {
    return *(int*)a - *(int*)b;
}

int* relativeSortArray(int* arr1, int arr1Size, int* arr2, int arr2Size, int* returnSize){
    *returnSize = arr1Size;
    int *hash = (int*)malloc(sizeof(int) * arr2Size);
    int cnt = 0;

    memset(hash, 0, sizeof(int) * arr2Size);

    for (int i = 0; i < arr2Size; i++) {
        for (int j = 0; j < arr1Size; j++) {
            if (arr2[i] == arr1[j]) {
                hash[i]++;
                arr1[j] = -1;
            } 
        }
    }

    qsort(arr1, arr1Size, sizeof(int), cmp);

    for (int i = 0; i < arr2Size; i++) {
        for (int j = 0; j < hash[i]; j++) {
            arr1[cnt] = arr2[i];
            cnt++;
        }
    }
    return arr1;
}
```