# LeetCode002. 两数相加
**
给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。
如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。
您可以假设除了数字 0 之外，这两个数都不会以 0 开头。
示例：
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807

**

```
struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2){
    int x, y, num, flag=0;
    struct ListNode *p = l1, *q = l2;
    struct ListNode *cur = (struct ListNode*)malloc(sizeof(struct ListNode));
    cur->next = NULL;
    struct ListNode *ret = cur;
    while(p!=NULL || q!=NULL)
    {
        x = (p!=NULL)?p->val:0;
        y = (q!=NULL)?q->val:0;
        num = x+y+flag;
        flag = num/10;
        cur->next = (struct ListNode*)malloc(sizeof(struct ListNode));
        cur = cur->next;
        cur->val = num%10;
        cur->next = NULL;
        if(p!=NULL)
            p = p->next;
        if(q!=NULL)
            q = q->next;
    }
    if(flag > 0)
    {
        cur->next = (struct ListNode*)malloc(sizeof(struct ListNode));
        cur = cur->next;
        cur->val = 1;
        cur->next = NULL;
    }
    return ret->next;
}

```