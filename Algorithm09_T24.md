# 算法学习篇（二）：链表03之交换节点

## 以leetcode24题为例

​		

### 一、算法原理

​		单链表的相邻节点之间两两交换，主要是对相邻节点的next指向的节点的彼此交换，以及和前序后序链表的连接。

​		指针cur指向当前节点，指针pre指向原链表当前节点cur的前一节点，并创建临时指针temp指向当前节点指针cur的下一节点。假定需要交换的两个节点为cur和temp分别指向的节点。

### 二、力扣原题

#### （1）[24. 两两交换链表中的节点](https://leetcode.cn/problems/swap-nodes-in-pairs/)

- 给你一个链表，两两交换其中相邻的节点，并返回交换后链表的头节点。你必须在不修改节点内部的值的情况下完成本题（即，只能进行节点交换）。

   

  **示例 1：**

  ![img](https://assets.leetcode.com/uploads/2020/10/03/swap_ex1.jpg)

  ```
  输入：head = [1,2,3,4]
  输出：[2,1,4,3]
  ```

  **示例 2：**

  ```
  输入：head = []
  输出：[]
  ```

  **示例 3：**

  ```
  输入：head = [1]
  输出：[1]
  ```

   

  **提示：**

  - 链表中节点的数目在范围 `[0, 100]` 内
  - `0 <= Node.val <= 100`



### 三、代码实现

#### （1）24题

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
    ListNode* swapPairs(ListNode* head) {
        ListNode *myHead = new ListNode(0);		//虚拟头节点
        myHead->next=head;						//虚拟头节点的next指向头节点
        ListNode *temp=nullptr;					//临时节点，初始化为空指针
        ListNode *cur=head;						//指向当前节点的指针，初始化为头节点，是交换节点之一（交换前前序）
        ListNode *pre=myHead;					//指向前序节点的指针，初始化为虚拟头节点
        while(cur!=nullptr&&cur->next!=nullptr)	//判断逻辑为当前节点为空指针，或当前节点的下一节点为空指针，意为交换完毕
        {
            temp=cur->next;						//temp为临时节点，是当前节点的下一节点，是交换节点之一（交换前后序）
            cur->next=temp->next;				//当前节点的下一节点指向临时节点的下一节点
            pre->next=temp;						//前序节点的下一节点指向当前节点的下一节点
            temp->next=cur;						//临时节点（交换前后序）的下一节点指向当前节点（交换前前序）
            pre=cur;							//下一次交换的前序节点移动到当前节点（交换后后序）
            cur=cur->next;						//当前节点移动到交换后当前节点（交换后后序）的下一节点
        }
        head=myHead->next;
        delete myHead;
        return head;
    }
};
```
