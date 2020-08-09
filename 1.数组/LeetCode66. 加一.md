# LeetCode66. 加一
**
给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。
最高位数字存放在数组的首位， 数组中每个元素只存储单个数字。
你可以假设除了整数 0 之外，这个整数不会以零开头。
示例 1:
输入: [1,2,3]
输出: [1,2,4]
解释: 输入数组表示数字 123。
示例 2:
输入: [4,3,2,1]
输出: [4,3,2,2]
解释: 输入数组表示数字 4321。
**
给出的题解是：最后一位加1，判断是否需要进位，如果首位进位需要分配一个比原数组大1的数组来存放最高位进位过后的数。
```
int* plusOne(int* digits, int digitsSize, int* returnSize){
	
	int i = digitsSize - 1;
	digits[i]++;
	while(digits[i] == 10)
    {
			
		i--;
		if(i == -1)
        {
			*returnSize = digitsSize + 1;
			int *res = (int *)malloc(sizeof(int) *(digitsSize+1));
			res[0] = 1;
			for(int j = 1; j < digitsSize+1;j++)
            {
				res[j] = 0;
			}
			return res;
		}
		
		digits[i]++;
	}
	
	for(int j = i+1; j < digitsSize; j++)
    {
		digits[j] = 0;
	}
	*returnSize = digitsSize;
	return digits;
}
```