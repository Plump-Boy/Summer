# LeetCode014. 最长公共前缀
**
编写一个函数来查找字符串数组中的最长公共前缀。
如果不存在公共前缀，返回空字符串 ""。
示例 1:
输入: ["flower","flow","flight"]
输出: "fl"
示例 2:
输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。
说明:
所有输入只包含小写字母 a-z 。
**
直接读取每一列的开头，相同继续，不同跳出，高效
```
char * longestCommonPrefix(char ** strs, int strsSize){
    if(strsSize==0) return "";  
    for(int i=0;i<strlen(strs[0]);i++)
    {   
        for(int j=1;j<strsSize;j++)
        {    
            if(strs[0][i]!=strs[j][i])
            { 
                strs[0][i]='\0';
                break;
            }
        }
    }
    return strs[0];
}
```