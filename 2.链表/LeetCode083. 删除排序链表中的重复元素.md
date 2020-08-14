# LeetCode083. 删除排序链表中的重复元素
**
给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次。
示例 1:
输入: 1->1->2
输出: 1->2
示例 2:
输入: 1->1->2->3->3
输出: 1->2->3
**
创建一个指针遍历链表，如果这一个和后一个相等，则删除，如果不等则向后移一位
```
struct ListNode* deleteDuplicates(struct ListNode* head){

	if(head == NULL)
		return head;
	struct ListNode *lp;
	struct ListNode *p = head;
	lp = p;
	while(p ->next != NULL){
		if(p -> val == p ->next -> val)
        {
			p -> next = p -> next -> next;
		}
		else
        {
			p = p -> next;
		}
	}
	return lp;
}
```