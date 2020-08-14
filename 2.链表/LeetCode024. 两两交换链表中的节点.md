# LeetCode024. 两两交换链表中的节点
**
给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。
你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。 
示例:
给定 1->2->3->4, 你应该返回 2->1->4->3.
**

```
struct ListNode* swapPairs(struct ListNode* head){
    if(head==0||head->next==0) return head;
    struct ListNode* odd=head, * even=odd->next;
    head=even;
    do{
        odd->next=even->next;
        even->next=odd;
        odd=odd->next;
        if(odd&&odd->next){
            even->next->next=odd->next;
            even=odd->next;
        }
        else break;
    } while(1);
    return head;
}
```