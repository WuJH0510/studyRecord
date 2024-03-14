# 算法学习篇（四）：滑动窗口

## 以leetcode209题为例

​		

### 一、算法原理

​		寻找子数组，可以通过滑动窗口的方式完成。

​		本质上是双指针算法，前指针往前遍历，后指针在数组大小大于等于目标数时向前移动，并更新数组和大小，以及对子数组长度进行判断。

### 二、力扣原题

#### （1）[209. 长度最小的子数组](https://leetcode.cn/problems/minimum-size-subarray-sum/)

给定一个含有 `n` 个正整数的数组和一个正整数 `target` **。**

找出该数组中满足其总和大于等于 `target` 的长度最小的 **连续**

**子数组**

`[numsl, numsl+1, ..., numsr-1, numsr]` ，并返回其长度**。**如果不存在符合条件的子数组，返回 `0` 。



**示例 1：**

```
输入：target = 7, nums = [2,3,1,2,4,3]
输出：2
解释：子数组 [4,3] 是该条件下的长度最小的子数组。
```

**示例 2：**

```
输入：target = 4, nums = [1,4,4]
输出：1
```

**示例 3：**

```
输入：target = 11, nums = [1,1,1,1,1,1,1,1]
输出：0
```

 

**提示：**

- `1 <= target <= 109`
- `1 <= nums.length <= 105`
- `1 <= nums[i] <= 105`



### 三、代码实现

#### （1）209题

以下是C++代码实现：

```c++
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int result=INT32_MAX;
        int sum=0;
        int begin=0;
        int length=0;
        for(int end=0;end<nums.size();end++)
        {
            sum+=nums[end];
            while(sum>=target)
            {
                length=end-begin+1;
                result=length<result?length:result;
                sum-=nums[begin++];
            }
        }
        return result==INT32_MAX?0:result;
    }
};
```
