# 算法学习篇（二）：链表02之反转链表

## 以leetcode206题为例

​		

### 一、算法原理

​		单链表的节点反转，可以通过双指针法完成。

​		其中一个指针指向当前节点，另一个指针指向反转后当前节点所要指向的下一节点，即原链表前一节点。

### 二、力扣原题

#### （1）[206. 反转链表](https://leetcode.cn/problems/reverse-linked-list/)

- 给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。

   

  **示例 1：**

  ![img](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

  ```
  输入：head = [1,2,3,4,5]
  输出：[5,4,3,2,1]
  ```

  **示例 2：**

  ![img](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg)

  ```
  输入：head = [1,2]
  输出：[2,1]
  ```

  **示例 3：**

  ```
  输入：head = []
  输出：[]
  ```

   

  **提示：**

  - 链表中节点的数目范围是 `[0, 5000]`
  - `-5000 <= Node.val <= 5000`



### 三、代码实现

#### （1）206题

以下是C++代码实现：

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode *temp=nullptr;		//保存当前节点的下一节点，以防原有链接断开
        ListNode *cur=head;			//保存当前节点
        ListNode *pre=nullptr;		//保存反转后当前节点的下一节点
        while(cur!=nullptr)			//是否反转完成
        {
            temp=cur->next;			//保存当前节点的下一节点，以防原有链接断开
            cur->next=pre;			//反转后链表当前节点的下一节点
            pre=cur;				//更新反转后链表当前节点的下一节点位置（为当前节点）
            cur=temp;				//更新当前节点位置（为当前节点的下一节点）
        }
        head=pre;					//更新头节点位置
        return head;
    }
};
```
