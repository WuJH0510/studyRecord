# 算法学习篇（一）：数组02之移除元素01

## 以leetcode27题，26题为例

​		

### 一、算法原理

​		该题目可以通过暴力解法完成，也可以通过双指针法完成。双指针法相对比较简洁。

​		暴力解法主要通过二重循环完成，第一层循环中每找到一个需要删除的元素，则在第二层循环中将所有元素往前移动一位，同时更新数组大小。

​		双指针法主要通过寻找与需要删除的元素不同的元素，即需要保留的元素更新原数组，此时通过一重循环即可实现。同时新数组的指针（慢指针）正好就是新数组的大小。

### 二、力扣原题

#### （1）[27. 移除元素](https://leetcode.cn/problems/remove-element/)

给你一个数组 `nums` 和一个值 `val`，你需要 **[原地](https://baike.baidu.com/item/原地算法)** 移除所有数值等于 `val` 的元素，并返回移除后数组的新长度。

不要使用额外的数组空间，你必须仅使用 `O(1)` 额外空间并 **[原地 ](https://baike.baidu.com/item/原地算法)修改输入数组**。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

 

**说明:**

为什么返回数值是整数，但输出的答案是数组呢?

请注意，输入数组是以**「引用」**方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

你可以想象内部操作如下:

```
// nums 是以“引用”方式传递的。也就是说，不对实参作任何拷贝
int len = removeElement(nums, val);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中 该长度范围内 的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

 

**示例 1：**

```
输入：nums = [3,2,2,3], val = 3
输出：2, nums = [2,2]
解释：函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。你不需要考虑数组中超出新长度后面的元素。例如，函数返回的新长度为 2 ，而 nums = [2,2,3,3] 或 nums = [2,2,0,0]，也会被视作正确答案。
```

**示例 2：**

```
输入：nums = [0,1,2,2,3,0,4,2], val = 2
输出：5, nums = [0,1,3,0,4]
解释：函数应该返回新的长度 5, 并且 nums 中的前五个元素为 0, 1, 3, 0, 4。注意这五个元素可为任意顺序。你不需要考虑数组中超出新长度后面的元素。
```

 

**提示：**

- `0 <= nums.length <= 100`
- `0 <= nums[i] <= 50`
- `0 <= val <= 100`



#### （2）[26. 删除有序数组中的重复项](https://leetcode.cn/problems/remove-duplicates-from-sorted-array/)

给你一个 **非严格递增排列** 的数组 `nums` ，请你**[ 原地](http://baike.baidu.com/item/原地算法)** 删除重复出现的元素，使每个元素 **只出现一次** ，返回删除后数组的新长度。元素的 **相对顺序** 应该保持 **一致** 。然后返回 `nums` 中唯一元素的个数。

考虑 `nums` 的唯一元素的数量为 `k` ，你需要做以下事情确保你的题解可以被通过：

- 更改数组 `nums` ，使 `nums` 的前 `k` 个元素包含唯一元素，并按照它们最初在 `nums` 中出现的顺序排列。`nums` 的其余元素与 `nums` 的大小不重要。
- 返回 `k` 。

**判题标准:**

系统会用下面的代码来测试你的题解:

```
int[] nums = [...]; // 输入数组
int[] expectedNums = [...]; // 长度正确的期望答案

int k = removeDuplicates(nums); // 调用

assert k == expectedNums.length;
for (int i = 0; i < k; i++) {
    assert nums[i] == expectedNums[i];
}
```

如果所有断言都通过，那么您的题解将被 **通过**。

 

**示例 1：**

```
输入：nums = [1,1,2]
输出：2, nums = [1,2,_]
解释：函数应该返回新的长度 2 ，并且原数组 nums 的前两个元素被修改为 1, 2 。不需要考虑数组中超出新长度后面的元素。
```

**示例 2：**

```
输入：nums = [0,0,1,1,1,2,2,3,3,4]
输出：5, nums = [0,1,2,3,4]
解释：函数应该返回新的长度 5 ， 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4 。不需要考虑数组中超出新长度后面的元素。
```

 

**提示：**

- `1 <= nums.length <= 3 * 104`
- `-104 <= nums[i] <= 104`
- `nums` 已按 **非严格递增** 排列



### 三、代码实现

#### （1）27题

以下是C++代码实现。

- 暴力破解法：

```c++
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int size = nums.size();
        for (int i = 0; i < size; i++) 
        {
            if (nums[i] == val) 
            { 
                for (int j = i + 1; j < size; j++)
                {
                    nums[j - 1] = nums[j];
                }
                i--;    // 因为下标i以后的数值都向前移动了一位，所以i也向前移动一位
                size--; // 此时数组的大小-1
            }
        }
        return size;
    }
};
```

- 双指针法：

```c++
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int fast=0,slow=0;				//原数组下标fast，更新后数组下标slow
        for(fast=0;fast<nums.size();fast++)
        {
            if(nums[fast]!=val)			//原数组中元素不等于要删除的值，放入更新后的数组中
            {
                nums[slow]=nums[fast];
                slow++;
            }
        }
        return slow;
    }
};
```

#### （2）26题

C++实现，此处使用双指针法实现。

```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int fast=1,slow=1;				//原数组下标fast，更新后数组下标slow
        for(fast=1;fast<nums.size();fast++)
        {
            if(nums[fast]!=nums[fast-1])//原数组中元素不等于前一个数组元素的值，需要记录到更新后的数组中。
            {
                nums[slow]=nums[fast];
                slow++;
            }
        }
        return slow;
    }
};
```

