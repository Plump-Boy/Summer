# LeetCode783. 二叉搜索树节点最小距离
**
给定一个二叉搜索树的根节点 root，返回树中任意两节点的差的最小值。
示例：
输入: root = [4,2,6,1,3,null,null]
输出: 1
解释:
注意，root是树节点对象(TreeNode object)，而不是数组。
给定的树 [4,2,6,1,3,null,null] 可表示为下图:
          4
        /   \
      2      6
     / \    
    1   3  
最小的差值是 1, 它是节点1和节点2的差值, 也是节点3和节点2的差值。
**
将树中所有节点的值写入数组，之后将数组排序。依次计算相邻数之间的差值，找出其中最小的值。
```
int min;
struct TreeNode* pre;

int InOrder(struct TreeNode* root){
    if(root==NULL)  return 0;
    InOrder(root->left);
    if(pre!=NULL){
        if(min>root->val-pre->val){
            min = root->val-pre->val;
        }
    }
    pre = root;
    InOrder(root->right);
    return 0;
}

int minDiffInBST(struct TreeNode* root){
    min = 0x3f3f3f3f;
    pre = NULL;
    InOrder(root);
    return min;   
}
```