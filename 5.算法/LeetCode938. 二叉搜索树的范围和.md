# LeetCode938. 二叉搜索树的范围和
**
给定二叉搜索树的根结点 root，返回 L 和 R（含）之间的所有结点的值的和。
二叉搜索树保证具有唯一的值。
示例 1：
输入：root = [10,5,15,3,7,null,18], L = 7, R = 15
输出：32
例 2：
输入：root = [10,5,15,3,7,13,18,1,null,6], L = 6, R = 10
输出：23
**
参考官方解法：我们对树进行深度优先搜索，对于当前节点 node，如果 node.val 小于等于 L，那么只需要继续搜索它的右子树；如果 node.val 大于等于 R，那么只需要继续搜索它的左子树；如果 node.val 在区间 (L, R) 中，则需要搜索它的所有子树。
```

int rangeSumBST(struct TreeNode* root, int L, int R){
    if(root == NULL)
        return 0;
    int sum = rangeSumBST(root ->left,L,R) + rangeSumBST (root -> right,L,R);
    if(root ->val <= R && root ->val >= L)
        sum += root ->val;
    return sum;

}
```