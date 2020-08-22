# LeetCode242. 有效的字母异位词
**
给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。
示例 1:
输入: s = "anagram", t = "nagaram"
输出: true
示例 2:
输入: s = "rat", t = "car"
输出: false
说明:
你可以假设字符串只包含小写字母。
**
如果是异位词，则排序后二者相同
```
bool isAnagram(char * s, char * t){
    int ns[26] = {0};
    int nt[26] = {0};
    int i;
    while(*s){
        ns[*s - 97] ++;
        s ++;
    }
    while(*t){
        nt[*t - 97] ++;
        t ++;
    }
    while(i < 26){
        if(ns[i] != nt[i]){
            return false;
        }
        ++ i;
    }
    return true;
}

```