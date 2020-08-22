# LeetCode125. 验证回文串
**
给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。
说明：本题中，我们将空字符串定义为有效的回文串。
示例 1:
输入: "A man, a plan, a canal: Panama"
输出: true
示例 2:
输入: "race a car"
输出: false
**
定义俩指针，分别从前和后开始比较
```
bool isPalindrome(char * s){
  int len = strlen(s);
  if (len == 0) return true;
  if (len == 1) return true;
  int i = 0, j = len - 1;
  while (i <= j) {
    int iv = s[i], jv = s[j];
    if (!(('0' <= iv && iv <= '9') || ('a' <= iv && iv <= 'z') || ('A' <= iv && iv <= 'Z'))) {
      i++;
      continue;
    }
    if (!(('0' <= jv && jv <= '9') || ('a' <= jv && jv <= 'z') || ('A' <= jv && jv <= 'Z'))) {
      j--;
      continue;
    }
    if (iv - jv == 0 || ((iv - jv) % 32 == 0 && iv >= 'A' && jv >= 'A')) {
      i++;
      j--;
    } else {
      return false;
    }
  }
  return true;
}
```