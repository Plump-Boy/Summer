# LeetCode058. 最后一个单词的长度
**
给定一个仅包含大小写字母和空格 ' ' 的字符串 s，返回其最后一个单词的长度。如果字符串从左向右滚动显示，那么最后一个单词就是最后出现的单词。
如果不存在最后一个单词，请返回 0 。
说明：一个单词是指仅由字母组成、不包含任何空格字符的 最大子字符串。
示例:
输入: "Hello World"
输出: 5
**
从后向前遍历，第一个不是空格的地方为end，再向前第一个为空格的为start，二者相减
```
int lengthOfLastWord(char * s){
    int end=strlen(s)-1;
    int start=0;
    int res=0;
   while(end>=0&&s[end]==' '){
            end--;
    }
    start=end;
    while(start>=0&&s[start]!=' '){
        start--;
    }
    res=end-start;
    return res;
}
```