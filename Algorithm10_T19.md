# 算法学习篇（六）：链表04之删除倒数第N个节点

## 以leetcode19题为例

​		

### 一、算法原理

​		对于这一类题，可以通过双指针法完成。

​		定义一个快指针和一个慢指针，首先让快指针往前移动n个节点，之后让快指针和慢指针同时往前移动，当快指针移动到链表最后一个节点时，慢指针正好指向需要删除的节点的前一个节点，此时可以进行删除节点操作。

### 二、力扣原题

#### （1）[19. 删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)

- 给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。

   

  **示例 1：**

  ![img](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

  ```
  输入：head = [1,2,3,4,5], n = 2
  输出：[1,2,3,5]
  ```

  **示例 2：**

  ```
  输入：head = [1], n = 1
  输出：[]
  ```

  **示例 3：**

  ```
  输入：head = [1,2], n = 1
  输出：[1]
  ```

   

  **提示：**

  - 链表中结点的数目为 `sz`
  - `1 <= sz <= 30`
  - `0 <= Node.val <= 100`
  - `1 <= n <= sz`



### 三、代码实现

#### （1）19题

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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* myHead=new ListNode(0);		//定义虚拟头节点
        myHead->next=head;
        ListNode* fast=myHead;					//定义快指针
        ListNode* slow=myHead;					//定义慢指针
        for(;n>0;n--)							//快指针往前移动n个节点
        {
            fast=fast->next;
        }
        while(fast->next!=nullptr)				//快指针慢指针同时移动，直到快指针指向链表最后一个节点
        {
            fast=fast->next;
            slow=slow->next;
        }
        ListNode *temp=slow->next;				//慢指针所在节点后一个节点是需要删除的节点，进行删除操作
        slow->next=temp->next;
        delete temp;
        head=myHead->next;
        delete myHead;
        return head;
    }
};
```
