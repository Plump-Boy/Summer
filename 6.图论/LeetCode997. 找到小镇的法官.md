# LeetCode997. 找到小镇的法官
**
在一个小镇里，按从 1 到 N 标记了 N 个人。传言称，这些人中有一个是小镇上的秘密法官。
如果小镇的法官真的存在，那么：
小镇的法官不相信任何人。
每个人（除了小镇法官外）都信任小镇的法官。
只有一个人同时满足属性 1 和属性 2 。
给定数组 trust，该数组由信任对 trust[i] = [a, b] 组成，表示标记为 a 的人信任标记为 b 的人。
如果小镇存在秘密法官并且可以确定他的身份，请返回该法官的标记。否则，返回 -1。
示例 1：
输入：N = 2, trust = [[1,2]]
输出：2
示例 2：
输入：N = 3, trust = [[1,3],[2,3]]
输出：3
示例 3：
输入：N = 3, trust = [[1,3],[2,3],[3,1]]
输出：-1
示例 4：
输入：N = 3, trust = [[1,2],[2,3]]
输出：-1
示例 5：
输入：N = 4, trust = [[1,3],[1,4],[2,3],[2,4],[4,3]]
输出：3
提示：
1 <= N <= 1000
trust.length <= 10000
trust[i] 是完全不同的
trust[i][0] != trust[i][1]
1 <= trust[i][0], trust[i][1] <= N
**
参考LeetCode上面的解法：遍历一次数组的第一个元素。找出不信任任何人的编号res；如果所有人都信任了其他人，返回-1；
2、遍历一次数组的第二个元素。如果N-1个人信任res，则返回res,否则返回-1.
```
int findJudge(int N, int** trust, int trustSize, int* trustColSize){
	int i, res = 0;
	int *map = (int*)calloc(N + 2, sizeof(int));
	for (i = 0; i < trustSize; i++)
		map[trust[i][0]]++;
	for (i = 1; i <= N; i++)
		if (!map[i]){
			res = i;
            break;
        }
	if (!res)
		return -1;                           
	memset(map, 0, sizeof(int)*(N + 2));
	for (i = 0; i < trustSize; i++)
		map[trust[i][1]]++;
	if (map[res] == N - 1)
		return res;
	return -1;
}
```