# LeetCode206. 反转链表
**
反转一个单链表。
示例
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
**

```
struct ListNode* reverseList(struct ListNode* head){
	struct ListNode *p = head, *r;
	head = NULL;
	while(p != NULL){
		r = p -> next;
		p -> next = head;
		head = p;
		p = r;
	}
	return head;
}
```