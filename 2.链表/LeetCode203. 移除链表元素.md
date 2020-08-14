# LeetCode203. 移除链表元素
**
删除链表中等于给定值 val 的所有节点。
示例:
输入: 1->2->6->3->4->5->6, val = 6
输出: 1->2->3->4->5
**

```
struct ListNode* removeElements(struct ListNode* head, int val){
    while(head!=NULL&&head->val==val) head=head->next;  
    struct ListNode* tmp=head;
    while(tmp!=NULL){
        if(tmp->next!=NULL&&tmp->next->val==val){
            tmp->next=tmp->next->next;  
        }
        else{
            tmp=tmp->next;
        }
    }
    return head;
}
```