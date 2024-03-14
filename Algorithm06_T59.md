# 算法学习篇（五）：旋转矩阵

## 以leetcode59题为例

​		

### 一、算法原理

​		本题关键在于抓住每次循环的特征，确定填入矩阵的数字起止位置，保证每轮循环固定填充四条边，并且保证是左闭右开区间。

​		为减少讨论，矩阵可初始化为输入数字的平方，以避免n为奇数时需要单独填入数字的情况。

### 二、力扣原题

#### （1）[59. 螺旋矩阵 II](https://leetcode.cn/problems/spiral-matrix-ii/)

给你一个正整数 `n` ，生成一个包含 `1` 到 `n2` 所有元素，且元素按顺时针顺序螺旋排列的 `n x n` 正方形矩阵 `matrix` 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg)

```
输入：n = 3
输出：[[1,2,3],[8,9,4],[7,6,5]]
```

**示例 2：**

```
输入：n = 1
输出：[[1]]
```

 

**提示：**

- `1 <= n <= 20`



### 三、代码实现

#### （1）59题

以下是C++代码实现：

```c++
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> result(n,vector<int>(n,n*n));
        int round=n/2;          //执行循环次数
        int x=0,y=0;            //每一圈循环初始位置
        int count=1;            //填入的数字
        int length=n-1;           //每次填入的长度
        for(;round!=0;round--,length--)
        {
            int i=x,j=y;
            for(;j<length;j++)
            {
                result[i][j]=count;
                count++;
            }
            for(;i<length;i++)
            {
                result[i][j]=count;
                count++;
            }
            for(;j>y;j--)
            {
                result[i][j]=count;
                count++;
            }
            for(;i>x;i--)
            {
                result[i][j]=count;
                count++;
            }
            x++;
            y++;
        }
        return result;
    }
};
```
