# LeetCode374. 猜数字大小
**
猜数字游戏的规则如下：
每轮游戏，系统都会从 1 到 n 随机选择一个数字。 请你猜选出的是哪个数字。
如果你猜错了，系统会告诉你，你猜测的数字比系统选出的数字是大了还是小了。
你可以通过调用一个预先定义好的接口 guess(int num) 来获取猜测结果，返回值一共有 3 种可能的情况（-1，1 或 0）：
-1 : 你猜测的数字比系统选出的数字大
 1 : 你猜测的数字比系统选出的数字小
 0 : 恭喜！你猜对了！
示例 :
输入: n = 10, pick = 6
输出: 6
**
直接使用二分查找，如果是-1则再向左边使用，是1则向右边使用
```
int guessNumber(int n){
	int start=1,end=n,mid,tmp;
    while(start<end)
    {
        mid=start+(end-start+1)/2;
        tmp=guess(mid);
        if(tmp==0)
        {
            return mid;
        }
        else if(tmp==-1)
        {
            end=mid-1;
        }
        else
        {
            start=mid+1;
        }
    }
    return start;
}
```