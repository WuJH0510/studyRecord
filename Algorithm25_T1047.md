# 算法学习篇（五）：栈与队列04之删除相邻重复项

## 以力扣1047题为例

​		

### 一、算法原理

​		可以利用栈完成这类问题。

​		当栈空或者遍历到的字符与栈顶不同，则将该字符入栈，若栈顶字符与遍历当前字符相同，则将字符出栈并跳过当前字符。

​		由于`string`类有`push_back()`和`pop_back()`这两个函数，可以通过`string`类直接实现栈的功能。

### 二、力扣原题

#### （1）[1047. 删除字符串中的所有相邻重复项](https://leetcode.cn/problems/remove-all-adjacent-duplicates-in-string/)

- 给出由小写字母组成的字符串 `S`，**重复项删除操作**会选择两个相邻且相同的字母，并删除它们。

  在 S 上反复执行重复项删除操作，直到无法继续删除。

  在完成所有重复项删除操作后返回最终的字符串。答案保证唯一。
  
   
  
**示例：**
  
  ```
  输入："abbaca"
  输出："ca"
  解释：
  例如，在 "abbaca" 中，我们可以删除 "bb" 由于两字母相邻且相同，这是此时唯一可以执行删除操作的重复项。之后我们得到字符串 "aaca"，其中又只有 "aa" 可以执行重复项删除操作，所以最后的字符串为 "ca"。
  ```
  
   
  
  **提示：**
  
  1. `1 <= S.length <= 20000`
  2. `S` 仅由小写英文字母组成。



### 三、代码实现

#### （1）1047题

以下是C++代码实现：

```c++
class Solution {
public:
    string removeDuplicates(string s) {
        string result;				//结果字符串
        for(int i=0;i<s.size();i++)	//遍历原字符串
        {
            if(result.empty()||s[i]!=result.back()) result.push_back(s[i]);		//空栈或与栈顶元素不同则字符入栈
            else result.pop_back();				//否则（当前元素与栈顶元素相同）则出栈
        }
        return result;
    }
};
```



