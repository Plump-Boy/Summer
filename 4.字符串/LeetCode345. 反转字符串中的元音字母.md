# LeetCode345. 反转字符串中的元音字母
**
编写一个函数，以字符串作为输入，反转该字符串中的元音字母。
示例 1:
输入: "hello"
输出: "holle"
示例 2:
输入: "leetcode"
输出: "leotcede"
说明:
元音字母不包含字母"y"。
**
双指针法
```
bool is_vowel(char ch)
{
    switch (ch) {
        case 'a': case 'A':
        case 'e': case 'E':
        case 'i': case 'I':
        case 'o': case 'O':
        case 'u': case 'U':
            return true;
        default:
            return false;
    }
}
char * reverseVowels(char * s)
{
    int first = 0;
    int last = strlen(s);
    while (first < last) {
        while (first < last && !is_vowel(s[first]))
            first++;
        while (first < last && !is_vowel(s[last]))
            last--;
        char tmp = s[first];
        s[first] = s[last];
        s[last] = tmp;
        first++;
        last--;
    }
    return s;
}
```