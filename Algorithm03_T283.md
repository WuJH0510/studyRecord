# 算法学习篇（一）：数组03之移除元素02

## 以leetcode283题为例

​		

### 一、算法原理

​		该题目可以通过暴力解法完成，也可以通过双指针法完成。双指针法相对比较简洁。

​		暴力解法主要通过二重循环完成，第一层循环中每找到一个需要删除的元素，则在第二层循环中将所有元素往前移动一位，同时更新数组大小。

​		双指针法主要通过寻找与需要删除的元素不同的元素，即需要保留的元素更新原数组，此时通过一重循环即可实现。同时新数组的指针（慢指针）正好就是新数组的大小。

### 二、力扣原题

#### （1）[283. 移动零](https://leetcode.cn/problems/move-zeroes/)

- 给定一个数组 `nums`，编写一个函数将所有 `0` 移动到数组的末尾，同时保持非零元素的相对顺序。

  **请注意** ，必须在不复制数组的情况下原地对数组进行操作。

   

  **示例 1:**

  ```
  输入: nums = [0,1,0,3,12]
  输出: [1,3,12,0,0]
  ```

  **示例 2:**

  ```
  输入: nums = [0]
  输出: [0]
  ```

   

  **提示**:

  - `1 <= nums.length <= 104`
  - `-231 <= nums[i] <= 231 - 1`

   

### 三、代码实现

#### （1）283题

以下是C++代码实现，采用双指针法：

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int fast=0,slow=0;
        for(fast=0;fast<nums.size();fast++) //快慢指针，更新非0元素
        {
            if(nums[fast]!=0)
            {
                nums[slow]=nums[fast];
                slow++;
            }
        }
        for(;slow<fast;slow++)   //处理末尾元素为0
        {
            nums[slow]=0;
        }
    }
};
```
