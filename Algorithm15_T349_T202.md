# 算法学习篇（三）：哈希表02之set结构的使用

## 以leetcode349、202题为例

​		

### 一、算法原理

​		通过STL当中的`unordered_set`结构可以比较方便的求解数组交集、快乐数等类型题目（元素是否重复出现类，适合哈希函数求解）。

### 二、力扣原题

#### （1）[349. 两个数组的交集](https://leetcode.cn/problems/intersection-of-two-arrays/)

给定两个数组 `nums1` 和 `nums2` ，返回 *它们的交集* 。输出结果中的每个元素一定是 **唯一** 的。我们可以 **不考虑输出结果的顺序** 。

 

**示例 1：**

```
输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2]
```

**示例 2：**

```
输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[9,4]
解释：[4,9] 也是可通过的
```

 

**提示：**

- `1 <= nums1.length, nums2.length <= 1000`
- `0 <= nums1[i], nums2[i] <= 1000`

 

#### （2）[202. 快乐数](https://leetcode.cn/problems/happy-number/)

编写一个算法来判断一个数 `n` 是不是快乐数。

 **「快乐数」** 定义为：

- 对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和。
- 然后重复这个过程直到这个数变为 1，也可能是 **无限循环** 但始终变不到 1。
- 如果这个过程 **结果为** 1，那么这个数就是快乐数。

如果 `n` 是 *快乐数* 就返回 `true` ；不是，则返回 `false` 。

### 三、代码实现

#### （1）349题

以下是C++代码实现：

```c++
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> result_set;		//定义结果集合
        unordered_set<int> nums_set(nums1.begin(),nums1.end());		//定义nums1的数据集合（每个数据仅出现1次）
        for(int num:nums2)					//C++11当中for循环在STL里的一种用法，（元素:容器），用于遍历容器中的元素
        {
            if(nums_set.find(num)!=nums_set.end())		//find函数如果没找到对应元素，返回该容器的end
            {
                result_set.insert(num);					//插入结果容器当中
            }
        }
        return vector<int>(result_set.begin(),result_set.end());	//转换为vector容器
    }
};
```

#### （2）202题

以下是C++代码实现：

```c++
class Solution {
public:
    int getSum(int n){					//求解每一位数平方和
        int sum=0;
        while(n)
        {
            sum+=(n%10)*(n%10);
            n=n/10;
        }
        return sum;
    }
    bool isHappy(int n) {
        unordered_set<int> res;			//定义集合
        while(true)
        {
            n=getSum(n);
            if(n==1) return true;		//平方和为1，返回true
            if(res.find(n)==res.end())	//未找到重复元素
                res.insert(n);			//插入集合当中
            else
                return false;			//找到重复出现数字，返回false
        }
    }
};
```

