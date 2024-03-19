# 算法学习篇（三）：哈希表01之有效的字母异位词

## 以leetcode242题、383题为例

​		

### 一、算法原理

​		假定字符固定为小写字母，可以通过定义一个数组，每位分别是对应字母出现的次数，若两次字母出现次数相同则代表是有效的字母异词。

​		对于赎金信问题也可类似解决。

### 二、力扣原题

#### （1）[242. 有效的字母异位词](https://leetcode.cn/problems/valid-anagram/)

- 给定两个字符串 `*s*` 和 `*t*` ，编写一个函数来判断 `*t*` 是否是 `*s*` 的字母异位词。

  **注意：**若 `*s*` 和 `*t*` 中每个字符出现的次数都相同，则称 `*s*` 和 `*t*` 互为字母异位词。

   

  **示例 1:**

  ```
  输入: s = "anagram", t = "nagaram"
  输出: true
  ```

  **示例 2:**

  ```
  输入: s = "rat", t = "car"
  输出: false
  ```

   

  **提示:**

  - `1 <= s.length, t.length <= 5 * 104`
  - `s` 和 `t` 仅包含小写字母

  

  

  #### （2）[383. 赎金信](https://leetcode.cn/problems/ransom-note/)

  给你两个字符串：`ransomNote` 和 `magazine` ，判断 `ransomNote` 能不能由 `magazine` 里面的字符构成。

  如果可以，返回 `true` ；否则返回 `false` 。

  `magazine` 中的每个字符只能在 `ransomNote` 中使用一次。

   

  **示例 1：**

  ```
  输入：ransomNote = "a", magazine = "b"
  输出：false
  ```

  **示例 2：**

  ```
  输入：ransomNote = "aa", magazine = "ab"
  输出：false
  ```

  **示例 3：**

  ```
  输入：ransomNote = "aa", magazine = "aab"
  输出：true
  ```

   

### 三、代码实现

#### （1）242题

以下是C++代码实现：

```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        vector<int> time(26,0);					//定义长度为26的数组
        if(s.size()!=t.size())return false;		//字符串长度不相等直接判错
        for(int i=0;i<s.size();i++)				//字符串s，对应字母出现则次数加1，字符串t则相反，对应字母出现则次数减1
        {
            time[s[i]-'a']++;
            time[t[i]-'a']--;
        }
        for(int i=0;i<time.size();i++)			//全部为0则判对，否则判错
        {
            if(time[i]!=0) return false;
        }
        return true;
    }
};
```

#### （2）383题

以下是C++代码实现：

```c++
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        vector<int> letter(26,0);
        for(int i=0;i<magazine.size();i++)
        {
            letter[magazine[i]-'a']++;
        }
        for(int i=0;i<ransomNote.size();i++)
        {
            letter[ransomNote[i]-'a']--;
        }
        for(int i=0;i<letter.size();i++)
        {
            if(letter[i]<0)
                return false;
        }
        return true;
    }
};
```

