# LeetCode687. 最长同值路径
**
给定一个二叉树，找到最长的路径，这个路径中的每个节点具有相同值。 这条路径可以经过也可以不经过根节点。
注意：两个节点之间的路径长度由它们之间的边数表示。
示例 1:
输入:
              5
             / \
            4   5
           / \   \
          1   1   5
输出:
2
示例 2:
输入:
              1
             / \
            4   5
           / \   \
          4   4   5
输出:
2
注意: 给定的二叉树不超过10000个结点。 树的高度不超过1000。
**
官方解法：我们可以将任何路径（具有相同值的节点）看作是最多两个从其根延伸出的箭头。

具体地说，路径的根将是唯一节点，因此该节点的父节点不会出现在该路径中，而箭头将是根在该路径中只有一个子节点的路径。

然后，对于每个节点，我们想知道向左延伸的最长箭头和向右延伸的最长箭头是什么？我们可以用递归来解决这个问题。

```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */

int getMax(int a, int b)
{
    if (a > b) {
        return a;
    }
    return b;
}

int getArrowLength(struct TreeNode* node, int* diagmeter) 
{
    if (node == NULL) {
        return 0;
    }

    int left = getArrowLength(node->left, diagmeter);
    int right = getArrowLength(node->right, diagmeter);

    int ArrowLeft = 0;
    int ArrowRight = 0;
    if ((node->left != NULL) && (node->val == node->left->val)) {
        ArrowLeft = 1 + left;
    }
    if ((node->right != NULL) && (node->val == node->right->val)) {
        ArrowRight = 1 + right;
    }

    *diagmeter = getMax(*diagmeter, ArrowLeft + ArrowRight);
    return getMax(ArrowLeft, ArrowRight);
}

int longestUnivaluePath(struct TreeNode* root) {
    int diagmeter = 0;
    getArrowLength(root, &diagmeter);
    return diagmeter;
}

```