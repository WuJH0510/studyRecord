# 算法学习篇（一）：数组04之左右指针

## 以leetcode977题为例

​		

### 一、算法原理

​		该题目除了平方后直接排序（暴力破解）外，还可以通过左右指针法完成。

​		由于原数组是大小有序的，平方后数组必然是两端大于中心元素，且由两端向中心递减。可以利用该特征边平方边排序。

### 二、力扣原题

#### （1）[977. 有序数组的平方](https://leetcode.cn/problems/squares-of-a-sorted-array/)

给你一个按 **非递减顺序** 排序的整数数组 `nums`，返回 **每个数字的平方** 组成的新数组，要求也按 **非递减顺序** 排序。



**示例 1：**

```
输入：nums = [-4,-1,0,3,10]
输出：[0,1,9,16,100]
解释：平方后，数组变为 [16,1,0,9,100]
排序后，数组变为 [0,1,9,16,100]
```

**示例 2：**

```
输入：nums = [-7,-3,2,3,11]
输出：[4,9,9,49,121]
```

 

**提示：**

- `1 <= nums.length <= 104`
- `-104 <= nums[i] <= 104`
- `nums` 已按 **非递减顺序** 排序



### 三、代码实现

#### （1）977题

以下是C++代码实现，采用左右指针法：

```c++
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        vector<int> result(nums.size(),0);		//结果数组
        int k=nums.size()-1;					//结果数组的下标，初始化为最大元素，从右往左输入
        int lPoint=0,rPoint=nums.size()-1;		//左指针设为0，右指针设为最大元素
        while(lPoint<=rPoint)
        {
            if(nums[lPoint]*nums[lPoint]<nums[rPoint]*nums[rPoint])	//右指针对应的平方数大于左指针
            {
                result[k--]=nums[rPoint]*nums[rPoint];				//原数组右指针平方输入结果数组，结果数组下标左移
                rPoint--;											//移动原数组右指针
            }
            else
            {
                result[k--]=nums[lPoint]*nums[lPoint];				//原数组左指针平方输入结果数组，结果数组下标左移
                lPoint++;											//移动原数组左指针
            }
        }
        return result;												//返回结果数组
    }
};
```
