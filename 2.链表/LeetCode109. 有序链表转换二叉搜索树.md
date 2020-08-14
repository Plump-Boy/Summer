# LeetCode109. 有序链表转换二叉搜索树

**
给定一个单链表，其中的元素按升序排序，将其转换为高度平衡的二叉搜索树。
本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1。
示例:
给定的有序链表： [-10, -3, 0, 5, 9],
一个可能的答案是：[0, -3, 9, -10, null, 5], 它可以表示下面这个高度平衡二叉搜索树：
      0
     / \
   -3   9
   /   /
 -10  5
**
借鉴于LeetCode题解
```
struct TreeNode* helper(int left,int right,int *nums){
    if(left >= right){
        return NULL;
    }
    int midpos = 0;
    midpos = (left+right)/2;
    struct TreeNode *node = malloc(sizeof(struct TreeNode));
    node->val = nums[midpos];
    node->left = helper(left,midpos,nums);
    node->right = helper(midpos+1,right,nums);

    return node;
}

struct TreeNode* sortedListToBST(struct ListNode* head){
    int nums[100000],numsSize=0;
    for(;head !=NULL;head = head->next){
        nums[numsSize] = head -> val;
        numsSize++;
    }
    return helper(0,numsSize,nums);
}
```