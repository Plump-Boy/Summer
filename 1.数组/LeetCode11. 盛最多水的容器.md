# LeetCode11. 盛最多水的容器
**
给你 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。
说明：你不能倾斜容器，且 n 的值至少为 2。
图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。
示例：
输入：[1,8,6,2,5,4,8,3,7]
输出：49
**
这道题一开始不会写，看了下leetcode上面的题解才勉强明白，设置双指针分别位于容器壁两端，根据规则移动指针，并且更新面积最大值 ，直到两指针相等 时返回 最大值。
```
int maxArea(int* height, int heightSize){
    int head = 0;
    int rear = heightSize - 1;
    int maxArea = 0;
    int tempArea = 0;

    while(head < rear)
    {
        tempArea = (rear - head) *                \
                   (height[head] > height[rear] ? \
                    height[rear] : height[head]);

        maxArea = (maxArea >= tempArea) ? maxArea : tempArea;

        if(height[head] >= height[rear])
        {
            rear--;
        }
        else
        {
            head++;
        }
    }

    return maxArea;

}
```