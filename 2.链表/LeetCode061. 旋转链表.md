# LeetCode061. 旋转链表
**
给定一个链表，旋转链表，将链表每个节点向右移动 k 个位置，其中 k 是非负数。
示例 1:
输入: 1->2->3->4->5->NULL, k = 2
输出: 4->5->1->2->3->NULL
解释:
向右旋转 1 步: 5->1->2->3->4->NULL
向右旋转 2 步: 4->5->1->2->3->NULL
示例 2:
输入: 0->1->2->NULL, k = 4
输出: 2->0->1->NULL
解释:
向右旋转 1 步: 2->0->1->NULL
向右旋转 2 步: 1->2->0->NULL
向右旋转 3 步: 0->1->2->NULL
向右旋转 4 步: 2->0->1->NULL
**
找出倒数第K+1个节点和倒数第一个节点，改变指针即可
```
struct ListNode* rotateRight(struct ListNode* head, int k){

    struct ListNode* first = head;
    struct ListNode* second = head;
    int len = 0;
    int i = 0;
    int newk = 0;
     if(head == NULL)
    {
        return NULL;
    }
    while(first!=NULL)
    {
        len++;
        first = first->next;
    }
    newk = k%len;
    first = head;
    while(first!=NULL && i<(newk+1-1))
    {
        first = first->next;
        i++;
    }
    while(first->next!=NULL)
    {
        first = first->next;
        second = second->next;
    }
    first->next = head;
    head = second->next;
    second->next = NULL;
    return head; 
}
```