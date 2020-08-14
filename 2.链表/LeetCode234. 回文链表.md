# LeetCode234. 回文链表
**
请判断一个链表是否为回文链表。
示例 1:
输入: 1->2
输出: false
示例 2:
输入: 1->2->2->1
输出: true
**
这个题没太看懂，借鉴的LeetCode上面的题解
```
bool isPalindrome(struct ListNode* head){
    if(head==0||head->next==0) return 1;
    struct ListNode* slow_p=head,* p=head;
    while(p->next!=0&&p->next->next!=0){
        slow_p=slow_p->next;
        p=p->next->next;
    }
    struct ListNode* head_=slow_p->next;
    slow_p->next=0;
    p=head_;
    while(p->next!=0){
        slow_p=head_;
        head_=p->next;
        p->next=p->next->next;
        head_->next=slow_p;
    }
    while(head_!=0){
        if(head->val!=head_->val) return 0;
        head=head->next;
        head_=head_->next;
    }
    return 1;
}

```