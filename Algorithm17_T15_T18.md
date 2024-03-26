# 算法学习篇（三）：哈希表04之双指针

## 以leetcode15、18题为例

​		

### 一、算法原理

​		对于三数之和与四数之和这两类问题，由于需要去重，用哈希法不合适，可以采用双指针法进行操作，核心思想在于利用双指针降低一次循环，即三数之和的时间复杂度降到`O(n²)`，四数之和的时间复杂度降到`O(n³)`，而快速排序的时间复杂度低于这两个算法的核心部分，故可先对数组进行排序。

​		三数之和题目中由于目标是0，第一个数只需大于0即可跳出循环。四数之和由于结果是个给定的数，可正可负，故判断逻辑应该为第一个数大于目标且第一个数大于0，并且四数之和在判断第2个数时，需要让下标减一大于第一个数的下标，并且把前两个数的和作为跳出循环的判断条件。

​		在判断后两个数时使用双指针法，具体是进行左右指针相向移动，并且左指针必然小于右指针（不能取等）。

### 二、力扣原题

#### （1）[15. 三数之和](https://leetcode.cn/problems/3sum/)

给你一个整数数组 `nums` ，判断是否存在三元组 `[nums[i], nums[j], nums[k]]` 满足 `i != j`、`i != k` 且 `j != k` ，同时还满足 `nums[i] + nums[j] + nums[k] == 0` 。请

你返回所有和为 `0` 且不重复的三元组。

**注意：**答案中不可以包含重复的三元组。

 

 

**示例 1：**

```
输入：nums = [-1,0,1,2,-1,-4]
输出：[[-1,-1,2],[-1,0,1]]
解释：
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0 。
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0 。
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0 。
不同的三元组是 [-1,0,1] 和 [-1,-1,2] 。
注意，输出的顺序和三元组的顺序并不重要。
```

**示例 2：**

```
输入：nums = [0,1,1]
输出：[]
解释：唯一可能的三元组和不为 0 。
```

**示例 3：**

```
输入：nums = [0,0,0]
输出：[[0,0,0]]
解释：唯一可能的三元组和为 0 。
```

 

**提示：**

- `3 <= nums.length <= 3000`
- `-105 <= nums[i] <= 105`

 

#### （2）[18. 四数之和](https://leetcode.cn/problems/4sum/)

给你一个由 `n` 个整数组成的数组 `nums` ，和一个目标值 `target` 。请你找出并返回满足下述全部条件且**不重复**的四元组 `[nums[a], nums[b], nums[c], nums[d]]` （若两个四元组元素一一对应，则认为两个四元组重复）：

- `0 <= a, b, c, d < n`
- `a`、`b`、`c` 和 `d` **互不相同**
- `nums[a] + nums[b] + nums[c] + nums[d] == target`

你可以按 **任意顺序** 返回答案 。

 

**示例 1：**

```
输入：nums = [1,0,-1,0,-2,2], target = 0
输出：[[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
```

**示例 2：**

```
输入：nums = [2,2,2,2,2], target = 8
输出：[[2,2,2,2]]
```

 

**提示：**

- `1 <= nums.length <= 200`
- `-109 <= nums[i] <= 109`
- `-109 <= target <= 109`



### 三、代码实现

#### （1）15题

以下是C++代码实现：

```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> result;
        sort(nums.begin(),nums.end());		//对原数组进行排序
        for(int i=0;i<nums.size();i++)		//遍历数组，首先挑选第一个元素
        {
            if(nums[i]>0)					//第1个元素最小，若大于0则返回结果
            { 
                return result;
            }
            if(i>0&&nums[i]==nums[i-1])		//对第1个元素去重，注意是对上一元素去重
            {
                continue;
            }
            int left=i+1;					//第2个元素，从第一个元素之后的下一元素开始遍历，双指针左指针
            int right=nums.size()-1;		//第3个元素，从数组最后开始遍历，双指针右指针
            while(right>left)				//由于第2和第3个元素必然不同，right必然大于left而不能等于
            {
                if(nums[i]+nums[left]+nums[right]>0) right--;		//三数之和大于0，移动右指针
                else if(nums[i]+nums[left]+nums[right]<0) left++;	//三数之和小于0，移动左指针
                else												//三数之和等于0
                {
                    result.push_back(vector<int>{nums[i],nums[left],nums[right]});	//记录到结果数组中
                    while(right>left&&nums[right]==nums[right-1])right--;			//对第3个元素的去重
                    while(right>left&&nums[left]==nums[left+1])left++;				//对第2个元素的去重
                    right--;														//左右指针各相向移动1个元素
                    left++;
                }
            }
        }
        return result;
    }
};
```

#### （2）18题

以下是C++代码实现：

```c++
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>> result;
        sort(nums.begin(),nums.end());			//对原数组进行排序
        for(int i=0;i<nums.size();i++)
        {
            if(nums[i]>target&&nums[i]>=0)		//对第1个数进行判断，满足条件即跳出循环
            {
                break;
            }
            if(i>0&&nums[i]==nums[i-1]) 		//对第1个数进行去重
            {
                continue;
            }
            for(int j=i+1;j<nums.size();j++)
            {
                if(nums[i]+nums[j]>target&&nums[i]+nums[j]>=0)	//对第2个数进行判断，满足条件即跳出循环
                {
                    break;
                }
                if(j>i+1&&nums[j]==nums[j-1])					//对第2个数进行去重
                {
                    continue;
                }
                int left=j+1,right=nums.size()-1;				//双指针
                while(left<right)
                {
                    if((long)nums[i]+nums[j]+nums[left]+nums[right]>target) right--;	//注意溢出问题
                    else if((long)nums[i]+nums[j]+nums[left]+nums[right]<target) left++;//进行类型转换到long
                    else																//对后两个数进行去重
                    {
                        result.push_back(vector<int>{nums[i],nums[j],nums[left],nums[right]});
                        while(left<right&&nums[left]==nums[left+1])left++;
                        while(left<right&&nums[right]==nums[right-1])right--;
                        left++;
                        right--;
                    }
                }
            }
        }
        return result;
    }
};
```

