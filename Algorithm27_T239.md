# 算法学习篇（五）：栈与队列06之单调队列

## 以力扣239题为例

​		

### 一、算法原理

​		单调队列在取最大值方面的应用是比较好的选择。

​		单调队列只需保证队列内部的值是单调递减，并管理最大值，即基于双端队列`deque`类下，有条件的`push`和`pop`操作。其中`push(int value)`操作时，需要将输入端（队列的`back`端）小于自身的值都从该端`pop`出去，再进行`push`操作；进行`pop`操作时则需要检查在滑动窗口（有效区域）末端的值是不是最大值（存放在队列的`front`端），即该值是否应该执行`pop`操作，如果是则从输出端（队列的`front`端）弹出。

### 二、力扣原题

#### （1）[239. 滑动窗口最大值](https://leetcode.cn/problems/sliding-window-maximum/)

- 给你一个整数数组 `nums`，有一个大小为 `k` 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 `k` 个数字。滑动窗口每次只向右移动一位。

  返回 *滑动窗口中的最大值* 。

   

  **示例 1：**

  ```
  输入：nums = [1,3,-1,-3,5,3,6,7], k = 3
  输出：[3,3,5,5,6,7]
  解释：
  滑动窗口的位置                最大值
  ---------------               -----
  [1  3  -1] -3  5  3  6  7       3
   1 [3  -1  -3] 5  3  6  7       3
   1  3 [-1  -3  5] 3  6  7       5
   1  3  -1 [-3  5  3] 6  7       5
   1  3  -1  -3 [5  3  6] 7       6
   1  3  -1  -3  5 [3  6  7]      7
  ```

  **示例 2：**

  ```
  输入：nums = [1], k = 1
  输出：[1]
  ```

   

  **提示：**

  - `1 <= nums.length <= 105`
  - `-104 <= nums[i] <= 104`
  - `1 <= k <= nums.length`



### 三、代码实现

#### （1）239题

以下是C++代码实现：

```c++
class Solution {
public:
    class Myqueue{					//定义单调队列类
    public:
        deque<int> que;				//基于双端队列
        void push(int value){		//输入数字，将小于应弹入队列的数字的值都从队列的输入端弹出
            while(!que.empty()&&value>que.back())
            {
                que.pop_back();
            }
            que.push_back(value);
        }
        void pop(int value){		//输出数字，若应该移出窗口的数字是队列内最大值，则从输出端弹出该数字
            if(!que.empty()&&value==que.front())
            {
                que.pop_front();
            }
        }
        int front(){				//返回队首元素，即最大值
            return que.front();
        }
    };
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        vector<int> result;
        Myqueue que;
        for(int i=0;i<k;i++)			//先将前k个数字入队列
        {
            que.push(nums[i]);
        }
        result.push_back(que.front());	//取第一组滑动窗口的最大值
        for(int i=k;i<nums.size();i++)	//往后依次输入输出数字
        {
            que.push(nums[i]);
            que.pop(nums[i-k]);
            result.push_back(que.front());
        }
        return result;
    }
};
```


