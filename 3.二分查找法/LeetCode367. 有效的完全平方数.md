# LeetCode367. 有效的完全平方数
**
给定一个正整数 num，编写一个函数，如果 num 是一个完全平方数，则返回 True，否则返回 False。
说明：不要使用任何内置的库函数，如  sqrt。
示例 1：
输入：16
输出：True
示例 2：
输入：14
输出：False
**
二分查找，在其中找平方后等于他的
```
bool isPerfectSquare(int num){
    long long int low=0,high=num/2+1,mid=0;

    while(low<=high){
        mid=(low+high)/2;

        if(mid*mid<num) low=mid+1;
        else if(mid*mid>num) high=mid-1;
        else break; 
    }
    if(low>high) return false;
    else return true;

}
```