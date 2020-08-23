# LeetCode874. 模拟行走机器人
**
机器人在一个无限大小的网格上行走，从点 (0, 0) 处开始出发，面向北方。该机器人可以接收以下三种类型的命令：
-2：向左转 90 度
-1：向右转 90 度
1 <= x <= 9：向前移动 x 个单位长度
在网格上有一些格子被视为障碍物。
第 i 个障碍物位于网格点  (obstacles[i][0], obstacles[i][1])
机器人无法走到障碍物上，它将会停留在障碍物的前一个网格方块上，但仍然可以继续该路线的其余部分。
返回从原点到机器人所有经过的路径点（坐标为整数）的最大欧式距离的平方。
示例 1：
输入: commands = [4,-1,3], obstacles = []
输出: 25
解释: 机器人将会到达 (3, 4)
示例 2：
输入: commands = [4,-1,4,-2,4], obstacles = [[2,4]]
输出: 65
解释: 机器人在左转走到 (1, 8) 之前将被困在 (1, 4) 处
提示：
0 <= commands.length <= 10000
0 <= obstacles.length <= 10000
-30000 <= obstacle[i][0] <= 30000
-30000 <= obstacle[i][1] <= 30000
答案保证小于 2 ^ 31
**
官方解法：思路

我们将一步步模拟机器人的路径。由于最多只有 90000 步，这足以通过给定的输入限制。

算法

我们将会存储机器人的位置和方向。如果机器人得到转弯的指令，我们就更新方向；否则就沿给定的方向走指定的步数。

必须注意使用 集合 Set 作为对障碍物使用的数据结构，以便我们可以有效地检查下一步是否受阻。如果不这样做，我们检查 该点是障碍点吗 可能会慢大约 10000 倍。

在某些语言中，我们需要将每个障碍物的坐标编码为 长整型 long 数据，以便它可以放入 集合 Set 数据结构中。或者，我们也可以将坐标编码为 字符串 string。

```
typedef struct{
	int a;
	int b;
}record_key;
typedef struct{
	record_key key;
	UT_hash_handle hh;
}Hash;
int robotSim(int* commands, int commandsSize, int** obstacles, int obstaclesSize, int* obstaclesColSize){
	int dir = 1, temp = 0, max = 0, *t = (int*)calloc(2, sizeof(int));
	Hash* map = NULL, *node = NULL, l;
	for (int i = 0; i < obstaclesSize; i++){
		node = NULL;
		memset(&l, 0, sizeof(Hash));
		l.key.a = obstacles[i][0];
		l.key.b = obstacles[i][1];
		HASH_FIND(hh, map, &l.key, sizeof(record_key), node);
		if (!node){
			node = (Hash*)malloc(sizeof(Hash));
			node->key.a = obstacles[i][0];
			node->key.b = obstacles[i][1];
			HASH_ADD(hh, map, key, sizeof(record_key), node);
		}
	}
	for (int i = 0; i < commandsSize; i++){
		if (commands[i] == -2)
			dir = (dir == 1) ? 4 : dir - 1;
		else if (commands[i] == -1)
			dir = (dir == 4) ? 1 : dir + 1;
		else{
			while (commands[i]--){
				if (dir == 1){
					t[1]++;
					node = NULL;
					memset(&l, 0, sizeof(Hash));
					l.key.a = t[0];
					l.key.b = t[1];
					HASH_FIND(hh, map, &l.key, sizeof(record_key), node);
					if (node){
						t[1]--;
						break;
					}
				}
				else if (dir == 2){
					t[0]++;
					node = NULL;
					memset(&l, 0, sizeof(Hash));
					l.key.a = t[0];
					l.key.b = t[1];
					HASH_FIND(hh, map, &l.key, sizeof(record_key), node);
					if (node){
						t[0]--;
						break;
					}
				}
				else if (dir == 3){
					t[1]--;
					node = NULL;
					memset(&l, 0, sizeof(Hash));
					l.key.a = t[0];
					l.key.b = t[1];
					HASH_FIND(hh, map, &l.key, sizeof(record_key), node);
					if (node){
						t[1]++;
						break;
					}
				}
				else{
					t[0]--;
					node = NULL;
					memset(&l, 0, sizeof(Hash));
					l.key.a = t[0];
					l.key.b = t[1];
					HASH_FIND(hh, map, &l.key, sizeof(record_key), node);
					if (node){
						t[0]++;
						break;
					}
				}
			}
		}
		temp = t[0] * t[0] + t[1] * t[1];
		max = max > temp ? max : temp;
	}
	return max;
}

```