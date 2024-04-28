# 算法学习篇（五）：栈与队列07之优先级队列、小顶堆

## 以力扣347题为例

​		

### 一、算法原理

​		优先级队列适合解决前k个最高频率的问题，可以先通过`map`结构将数据和出现频率进行映射，然后根据出现频率，利用小顶堆（优先级队列实现）迭代，只保留前k个结果，超出k个则从队列中输出。最后逆序输出到数组中，返回结果。

### 二、力扣原题

#### （1）[347. 前 K 个高频元素](https://leetcode.cn/problems/top-k-frequent-elements/)

- 给你一个整数数组 `nums` 和一个整数 `k` ，请你返回其中出现频率前 `k` 高的元素。你可以按 **任意顺序** 返回答案。

   

  **示例 1:**

  ```
  输入: nums = [1,1,1,2,2,3], k = 2
  输出: [1,2]
  ```

  **示例 2:**

  ```
  输入: nums = [1], k = 1
  输出: [1]
  ```

   

  **提示：**

  - `1 <= nums.length <= 105`
  - `k` 的取值范围是 `[1, 数组中不相同的元素的个数]`
  - 题目数据保证答案唯一，换句话说，数组中前 `k` 个高频元素的集合是唯一的

   

  **进阶：**你所设计算法的时间复杂度 **必须** 优于 `O(n log n)` ，其中 `n` 是数组大小。



### 三、代码实现

#### （1）347题

以下是C++代码实现：

```c++
class Solution {
public:
    struct myComp{								//定义比较规则（结构体和类都可以）
        bool operator() (const pair<int,int>&lhs,const pair<int,int>&rhs){
            return lhs.second>rhs.second;		//左大于右是小顶堆，右大于左是大顶堆
        }
    };
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int,int> map;				//定义无序映射
        for(int i:nums)							//统计各个元素出现频率
        {
            map[i]++;
        }
        priority_queue<pair<int,int>,vector<pair<int,int>>,myComp> pri_que;	//定义优先级队列作为小顶堆
        for(unordered_map<int,int>::iterator it=map.begin();it!=map.end();it++)
        {										//遍历并进行优先级排序
            pri_que.push(*it);
            if(pri_que.size()>k)				//只保留频率为前k个的数据，其余数据会被弹出
            pri_que.pop();
        }
        vector<int> result(k);
        for(int i=k-1;i>=0;i--)					//逆序输出结果到数组中
        {
            result[i]=pri_que.top().first;
            pri_que.pop();
        }
        return result;
    }
};
```


