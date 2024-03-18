# 算法学习篇（二）：链表06之环形链表

## 以leetcode142题为例

​		

### 一、算法原理

​		本题目需要检测链表当中是否存在环的结构，如果有环则返回环的入口。

​		可以通过快慢指针法寻找环，具体是快指针一次移动两个节点，慢指针一次移动一个节点，当快指针和慢指针的节点地址相同时，表明存在环，若快指针（对于无环链表而言，快指针先到末尾）本身为空指针或指向空指针，则表明该链表无环。

​		当快指针和慢指针相遇后，我们设链表头节点到环的入口节点的距离为`x`，环的入口节点到快慢指针相遇节点的距离为`y`，相遇节点往后至环的入口节点的距离为`z`，设快指针移动`n`圈才与慢指针相遇。相遇时，由于快指针一次移动2个节点，慢指针一次移动1个节点，快指针移动的距离是慢指针移动的2倍，对应的关系式为：
$$
2(x+y)=x+y+n(y+z)
$$
​		两边同时去掉一个`x+y`，由于需要求的是环的入口，则需要知道`x`的值，移动`y`之后得到关系式：
$$
x=n(y+z)-y
$$
​		即：
$$
x=(n-1)(y+z)+z
$$
​		要使快慢指针相遇，`n`必然大于等于`1`，当`n=1`时，`x=z`，对应的`n>1`时，由于`y+z`为环的长度，若两指针移动速度相等，即可忽略不计。因此可使两指针的其中一个指针移动到头节点，另一指针仍在原有位置，此时两指针同时移动，一次移动1个节点，当两指针相遇（指向节点地址相同）时，该节点便为链表环部分的入口。

### 二、力扣原题

#### （1）[142. 环形链表 II](https://leetcode.cn/problems/linked-list-cycle-ii/)

- 给定一个链表的头节点  `head` ，返回链表开始入环的第一个节点。 *如果链表无环，则返回 `null`。*

  如果链表中有某个节点，可以通过连续跟踪 `next` 指针再次到达，则链表中存在环。 为了表示给定链表中的环，评测系统内部使用整数 `pos` 来表示链表尾连接到链表中的位置（**索引从 0 开始**）。如果 `pos` 是 `-1`，则在该链表中没有环。**注意：`pos` 不作为参数进行传递**，仅仅是为了标识链表的实际情况。

  **不允许修改** 链表。

  

   

  **示例 1：**

  ![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

  ```
  输入：head = [3,2,0,-4], pos = 1
  输出：返回索引为 1 的链表节点
  解释：链表中有一个环，其尾部连接到第二个节点。
  ```

  **示例 2：**

  ![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test2.png)

  ```
  输入：head = [1,2], pos = 0
  输出：返回索引为 0 的链表节点
  解释：链表中有一个环，其尾部连接到第一个节点。
  ```

  **示例 3：**

  ![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test3.png)

  ```
  输入：head = [1], pos = -1
  输出：返回 null
  解释：链表中没有环。
  ```

   

  **提示：**

  - 链表中节点的数目范围在范围 `[0, 104]` 内
  - `-105 <= Node.val <= 105`
  - `pos` 的值为 `-1` 或者链表中的一个有效索引

   



### 三、代码实现

#### （1）142题

以下是C++代码实现：

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode *fast=head;					//定义快慢指针，均指向头节点
        ListNode *slow=head;
        while(fast!=NULL&&fast->next!=NULL)		//快指针未到无环链表末尾时（因一次移动2个节点，
            									//需要同时检测该指针本身以及其next域）
        {
            fast=fast->next->next;				//快指针一次移动2个节点
            slow=slow->next;					//慢指针一次移动1个节点
            if(fast==slow)						//地址相同，发现环
            {
                fast=head;						//假定快指针移动到头节点
                while(fast!=slow)				//快指针与慢指针移动到相同地址时，该节点就是环的入口
                {
                    fast=fast->next;			//两个指针一次移动1个节点
                    slow=slow->next;
                }
                return fast;
            }
        }
        return NULL;
    }
};
```
