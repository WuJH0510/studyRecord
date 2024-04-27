# 算法学习篇（五）：栈与队列01之用栈模拟队列

## 以力扣232题为例

​		

### 一、算法原理

​		可以设计一个输入栈和一个输出栈，通过对这两个栈的操作模拟队列的操作。		

### 二、力扣原题

#### （1）[232. 用栈实现队列](https://leetcode.cn/problems/implement-queue-using-stacks/)

请你仅使用两个栈实现先入先出队列。队列应当支持一般队列支持的所有操作（`push`、`pop`、`peek`、`empty`）：

实现 `MyQueue` 类：

- `void push(int x)` 将元素 x 推到队列的末尾
- `int pop()` 从队列的开头移除并返回元素
- `int peek()` 返回队列开头的元素
- `boolean empty()` 如果队列为空，返回 `true` ；否则，返回 `false`

**说明：**

- 你 **只能** 使用标准的栈操作 —— 也就是只有 `push to top`, `peek/pop from top`, `size`, 和 `is empty` 操作是合法的。
- 你所使用的语言也许不支持栈。你可以使用 list 或者 deque（双端队列）来模拟一个栈，只要是标准的栈操作即可。

 

**示例 1：**

```
输入：
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
输出：
[null, null, null, 1, 1, false]

解释：
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false
```



 

**提示：**

- `1 <= x <= 9`
- 最多调用 `100` 次 `push`、`pop`、`peek` 和 `empty`
- 假设所有操作都是有效的 （例如，一个空的队列不会调用 `pop` 或者 `peek` 操作）



### 三、代码实现

#### （1）232题

以下是C++代码实现：

```c++
class MyQueue {
public:
    stack<int> stIn;		//输入栈
    stack<int> stOut;		//输出栈
    MyQueue() {

    }
    
    void push(int x) {				//输入元素到输入栈中
        stIn.push(x);
    }
    
    int pop() {
        if(stOut.empty())			//若输出栈为空，从输入栈中导入全部元素
        {
            while(!stIn.empty())	//输入栈非空时导入数据
            {
                stOut.push(stIn.top());
                stIn.pop();
            }
        }
        int result = stOut.top();	//从输出栈输出数据
        stOut.pop();
        return result;
    }
    
    int peek() {
        int result=this->pop();		//直接应用已有pop函数操作
        stOut.push(result);			//将查阅的队首元素放回到输出栈中
        return result;
    }
    
    bool empty() {
        return stIn.empty()&&stOut.empty();	//输入栈和输出栈都为空时模拟队列为空
    }
};

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue* obj = new MyQueue();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->peek();
 * bool param_4 = obj->empty();
 */
```



