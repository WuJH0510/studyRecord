# 算法学习篇（五）：栈与队列02之用队列模拟栈

## 以力扣225题为例

​		

### 一、算法原理

​		只需要一个队列即可完成对栈的模拟。重点在于`pop()`时，除最后一个元素之外，其余元素每输出一个便输入原队列。	

### 二、力扣原题

#### （1）[225. 用队列实现栈](https://leetcode.cn/problems/implement-stack-using-queues/)

- 请你仅使用两个队列实现一个后入先出（LIFO）的栈，并支持普通栈的全部四种操作（`push`、`top`、`pop` 和 `empty`）。

  实现 `MyStack` 类：

  - `void push(int x)` 将元素 x 压入栈顶。
  - `int pop()` 移除并返回栈顶元素。
  - `int top()` 返回栈顶元素。
  - `boolean empty()` 如果栈是空的，返回 `true` ；否则，返回 `false` 。

   

  **注意：**

  - 你只能使用队列的标准操作 —— 也就是 `push to back`、`peek/pop from front`、`size` 和 `is empty` 这些操作。
  - 你所使用的语言也许不支持队列。 你可以使用 list （列表）或者 deque（双端队列）来模拟一个队列 , 只要是标准的队列操作即可。

   

  **示例：**

  ```
  输入：
  ["MyStack", "push", "push", "top", "pop", "empty"]
  [[], [1], [2], [], [], []]
  输出：
  [null, null, null, 2, 2, false]
  
  解释：
  MyStack myStack = new MyStack();
  myStack.push(1);
  myStack.push(2);
  myStack.top(); // 返回 2
  myStack.pop(); // 返回 2
  myStack.empty(); // 返回 False
  ```

   

  **提示：**

  - `1 <= x <= 9`
  - 最多调用`100` 次 `push`、`pop`、`top` 和 `empty`
  - 每次调用 `pop` 和 `top` 都保证栈不为空

   

  **进阶：**你能否仅用一个队列来实现栈。



### 三、代码实现

#### （1）225题

以下是C++代码实现：

```c++
class MyStack {
public:
    queue<int> que1;
    MyStack() {

    }
    
    void push(int x) {				//输入模拟栈
        que1.push(x);
    }
    
    int pop() {
        int size=que1.size();
        while(size>1)				//除最后一个元素外，其余元素先出队列再入队列
        {
            que1.push(que1.front());
            que1.pop();
            size--;
        }
        int result=que1.front();	//此时队首元素就是栈顶元素，输出
        que1.pop();
        return result;
    }
    
    int top() {
        return que1.back();			//返回队列尾部元素作为栈顶元素
    }
    
    bool empty() {
        return que1.empty();		//队列为空则模拟栈为空
    }
};

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack* obj = new MyStack();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->top();
 * bool param_4 = obj->empty();
 */
```



