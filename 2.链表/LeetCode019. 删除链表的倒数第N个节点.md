# LeetCode019. 删除链表的倒数第N个节点
**
给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。
示例：
给定一个链表: 1->2->3->4->5, 和 n = 2.
当删除了倒数第二个节点后，链表变为 1->2->3->5.
说明：
给定的 n 保证是有效的。
**
双指针
```
struct ListNode* removeNthFromEnd(struct ListNode* head, int n){
    struct ListNode *p,*q,*dev;
    dev=(struct ListNode*)malloc(sizeof(struct ListNode));
    dev->val=0;
    dev->next=head;
    p=dev;
    q=dev;
    int cnt=0;
    while(p){
        cnt++;
        p=p->next;
        if(cnt>n+1)
            q=q->next;
    }
    q->next=q->next->next;
    return dev->next;
}

```