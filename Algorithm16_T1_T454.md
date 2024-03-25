# 算法学习篇（三）：哈希表03之map的使用

## 以leetcode1、454题为例

​		

### 一、算法原理

​		通过STL当中的`unordered_map`结构可以比较方便的求解两数之和，四数相加类的问题。

​		对于两数之和，可以把遍历过程中未找到配对的数字及其下标作为一对存进map中，遍历`nums[i]`时在map中寻找目标数字,即`target-nums[i]`，匹配到则返回两数的下标。

​		对于四数相加，由于四个数均出现在不同的数组中，因此可以把4个数组两两配对，前两个数组的所有数字之和以及出现次数作为一对，存放在map结构中，在遍历后两个数组时，则可以在map中寻找目标数，即`0-c-d`，每找到一组则加上对应记录的次数。

### 二、力扣原题

#### （1）[1. 两数之和](https://leetcode.cn/problems/two-sum/)

- 给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** *`target`* 的那 **两个** 整数，并返回它们的数组下标。

  你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

  你可以按任意顺序返回答案。

   

  **示例 1：**

  ```
  输入：nums = [2,7,11,15], target = 9
  输出：[0,1]
  解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
  ```

  **示例 2：**

  ```
  输入：nums = [3,2,4], target = 6
  输出：[1,2]
  ```

  **示例 3：**

  ```
  输入：nums = [3,3], target = 6
  输出：[0,1]
  ```

   

  **提示：**

  - `2 <= nums.length <= 104`
  - `-109 <= nums[i] <= 109`
  - `-109 <= target <= 109`
  - **只会存在一个有效答案**

 

#### （2）[454. 四数相加 II](https://leetcode.cn/problems/4sum-ii/)

给你四个整数数组 `nums1`、`nums2`、`nums3` 和 `nums4` ，数组长度都是 `n` ，请你计算有多少个元组 `(i, j, k, l)` 能满足：

- `0 <= i, j, k, l < n`
- `nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0`

 

**示例 1：**

```
输入：nums1 = [1,2], nums2 = [-2,-1], nums3 = [-1,2], nums4 = [0,2]
输出：2
解释：
两个元组如下：
1. (0, 0, 0, 1) -> nums1[0] + nums2[0] + nums3[0] + nums4[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> nums1[1] + nums2[1] + nums3[0] + nums4[0] = 2 + (-1) + (-1) + 0 = 0
```

**示例 2：**

```
输入：nums1 = [0], nums2 = [0], nums3 = [0], nums4 = [0]
输出：1
```

 

 **提示：**

- `n == nums1.length`
- `n == nums2.length`
- `n == nums3.length`
- `n == nums4.length`
- `1 <= n <= 200`
- `-228 <= nums1[i], nums2[i], nums3[i], nums4[i] <= 228`



### 三、代码实现

#### （1）1题

以下是C++代码实现：

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int> map;					//映射结构，用于保存已遍历过且未找到的数字及其下标对
        for(int i=0;i<nums.size();i++)				//遍历数组
        {
            auto iter=map.find(target-nums[i]);		//定义迭代器为map的find结果值
            if(iter!=map.end())						//若找到则直接返回两数字的下标
            {
                return {iter->second,i};
            }
            map.insert(pair<int,int>(nums[i],i));	//若未找到则将当前数字及其下标对加入映射中
        }
        return {};
    }
};
```

#### （2）454题

以下是C++代码实现：

```c++
class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
        unordered_map<int,int> map;
        int count=0;
        for(int a:nums1)
            for(int b:nums2)		//遍历数组1和数组2，把数组1,2中元素的和及其对应出现的次数记录在map中
            {
                map[a+b]++;
            }
        for(int c:nums3)
            for(int d:nums4)		//遍历数组3和数组4，在映射中寻找0与数组3,4中元素的和相减的目标数及其出现的次数
            {
                if(map.find(0-c-d)!=map.end())
                    count+=map[0-c-d];
            }
        return count;
    }
};
```

