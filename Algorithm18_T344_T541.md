# 算法学习篇（四）：字符串01之反转字符串

## 以leetcode344、541题为例

​		

### 一、算法原理

​		字符串的基本操作，反转字符串。可以通过数组元素对位对换完成。

### 二、力扣原题

#### （1）[344. 反转字符串](https://leetcode.cn/problems/reverse-string/)

编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 `s` 的形式给出。

不要给另外的数组分配额外的空间，你必须**[原地](https://baike.baidu.com/item/原地算法)修改输入数组**、使用 O(1) 的额外空间解决这一问题。

 

**示例 1：**

```
输入：s = ["h","e","l","l","o"]
输出：["o","l","l","e","h"]
```

**示例 2：**

```
输入：s = ["H","a","n","n","a","h"]
输出：["h","a","n","n","a","H"]
```

 

**提示：**

- `1 <= s.length <= 105`
- `s[i]` 都是 [ASCII](https://baike.baidu.com/item/ASCII) 码表中的可打印字符

 

#### （2）[541. 反转字符串 II](https://leetcode.cn/problems/reverse-string-ii/)

给定一个字符串 `s` 和一个整数 `k`，从字符串开头算起，每计数至 `2k` 个字符，就反转这 `2k` 字符中的前 `k` 个字符。

- 如果剩余字符少于 `k` 个，则将剩余字符全部反转。
- 如果剩余字符小于 `2k` 但大于或等于 `k` 个，则反转前 `k` 个字符，其余字符保持原样。

 

**示例 1：**

```
输入：s = "abcdefg", k = 2
输出："bacdfeg"
```

**示例 2：**

```
输入：s = "abcd", k = 2
输出："bacd"
```

 

**提示：**

- `1 <= s.length <= 104`
- `s` 仅由小写英文组成
- `1 <= k <= 104`



### 三、代码实现

#### （1）344题

以下是C++代码实现：

```c++
class Solution {
public:
    void reverseString(vector<char>& s) {
        for(int i=0,j=s.size()-1;i<s.size()/2;i++,j--)		//注意对换元素的范围
        {
            swap(s[i],s[j]);								//数组对位交换元素
        }
    }
};
```

#### （2）541题

以下是C++代码实现：

```c++
class Solution {
public:
    string reverseStr(string s, int k) {
        for(int i=0;i<s.size();i+=2*k)					//以2*k个字符为单位进行对换
        {
            if(i+k<=s.size())
                reverse(s.begin()+i,s.begin()+i+k);		//若i+k小于字符串长度，即未到字符串末端
            else
                reverse(s.begin()+i,s.end());			//若i+k大于于字符串长度，即已到字符串末端
        }
        return s;
    }
};
```

