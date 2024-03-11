# 算法学习篇（一）：二分查找（折半查找）01

## 以leetcode704题、35题为例

​		

### 一、算法原理

​		给定一个元素**有序**的数组（假定单调递增），且数组中各个元素无重复，给定一个数值，需要查找到数组中与之匹配的元素，并返回其在数组中的下标。二分法首先寻找给定数组的中心下标位置的值，通过给定数值与给定数组中心下标（左值+（右值-左值）/2）的元素的大小的比较，确定元素所在区间（左半区间，中心下标值，右半区间），并反复进行这一过程，实现对元素的查找。

### 二、力扣原题

#### （1）[704. 二分查找](https://leetcode.cn/problems/binary-search/)

给定一个 `n` 个元素有序的（升序）整型数组 `nums` 和一个目标值 `target` ，写一个函数搜索 `nums` 中的 `target`，如果目标值存在返回下标，否则返回 `-1`。


**示例 1:**

```
输入: nums = [-1,0,3,5,9,12], target = 9
输出: 4
解释: 9 出现在 nums 中并且下标为 4
```

**示例 2:**

```
输入: nums = [-1,0,3,5,9,12], target = 2
输出: -1
解释: 2 不存在 nums 中因此返回 -1
```

 

**提示：**

1. 你可以假设 `nums` 中的所有元素是不重复的。
2. `n` 将在 `[1, 10000]`之间。
3. `nums` 的每个元素都将在 `[-9999, 9999]`之间。



#### （2）[35. 搜索插入位置](https://leetcode.cn/problems/search-insert-position/)

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

请必须使用时间复杂度为 `O(log n)` 的算法。

 

**示例 1:**

```
输入: nums = [1,3,5,6], target = 5
输出: 2
```

**示例 2:**

```
输入: nums = [1,3,5,6], target = 2
输出: 1
```

**示例 3:**

```
输入: nums = [1,3,5,6], target = 7
输出: 4
```

 

**提示:**

- `1 <= nums.length <= 104`
- `-104 <= nums[i] <= 104`
- `nums` 为 **无重复元素** 的 **升序** 排列数组
- `-104 <= target <= 104`



### 三、代码实现

#### （1）704题

以下是C++代码实现。

```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left=0;								//左值下标
        int right=nums.size()-1;				//右值下标
        while(left<=right)						//有效区间被定义为闭区间
        {
            int middle=left+(right-left)/2;		//中心下标值
            if(nums[middle]<target)
                left=middle+1;					//取右区间进行迭代，更改左值下标
            else if(nums[middle]>target)
                right=middle-1;					//取左区间进行迭代，更改右值下标
            else return middle;					//与中心值相等，返回中心值下标
        }
        return -1;								//查找失败返回-1
    }
};
```

#### （2）35题

以下是C++代码实现

```c++
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int left=0;								//左值下标
        int right=nums.size()-1;				//右值下标
        int middle;								//中心下标值
        while(left<=right)						//有效区间被定义为闭区间
        {
            middle=left+(right-left)/2;			//中心下标值跟随循环更新
            if(nums[middle]<target)
                left=middle+1;					//取右区间进行迭代，更改左值下标
            else if(nums[middle]>target)
                right=middle-1;					//取左区间进行迭代，更改右值下标
            else return middle;					//与中心值相等，返回中心值下标
        }
        if(nums[middle]>target) return middle;
        else return middle+1;
    }
};
```

