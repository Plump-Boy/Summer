# LeetCode082. 删除排序链表中的重复元素 II
**
给定一个排序链表，删除所有含有重复数字的节点，只保留原始链表中 没有重复出现 的数字。
示例 1:
输入: 1->2->3->3->4->4->5
输出: 1->2->5
示例 2:
输入: 1->1->1->2->3
输出: 2->3
**

```
struct ListNode* deleteDuplicates(struct ListNode* head){
    struct ListNode* dummyHead = (struct ListNode*)calloc(1, sizeof(struct ListNode));
    dummyHead -> next = head;
    struct ListNode* squEnd = dummyHead;
    struct ListNode* cur = head; 
    struct ListNode* delNode = NULL;
    while(cur != NULL && cur -> next != NULL){
        if(cur -> val == cur -> next -> val){
            while(cur -> next != NULL && cur -> val == cur -> next -> val){
                delNode = cur; 
                cur = cur -> next;
                free(delNode);
            }
            delNode = cur;
            cur = cur -> next;
            squEnd -> next = cur;
            free(delNode);
        }else{
            squEnd = cur; 
            cur = cur -> next;
        }
        
    }
    struct ListNode* ret = dummyHead -> next;
    free(dummyHead);
    return ret;
}
```