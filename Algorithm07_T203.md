# 算法学习篇（二）：链表01之删除元素

## 以leetcode203题为例

​		

### 一、算法原理

​		单链表的元素删除，可以增设一个虚拟头结点，保证删除实际头结点的操作一致性。

### 二、力扣原题

#### （1）[203. 移除链表元素](https://leetcode.cn/problems/remove-linked-list-elements/)

- 给你一个链表的头节点 `head` 和一个整数 `val` ，请你删除链表中所有满足 `Node.val == val` 的节点，并返回 **新的头节点** 。

   

  **示例 1：**

  ![img](https://assets.leetcode.com/uploads/2021/03/06/removelinked-list.jpg)

  ```
  输入：head = [1,2,6,3,4,5,6], val = 6
  输出：[1,2,3,4,5]
  ```

  **示例 2：**

  ```
  输入：head = [], val = 1
  输出：[]
  ```

  **示例 3：**

  ```
  输入：head = [7,7,7,7], val = 7
  输出：[]
  ```

   

  **提示：**

  - 列表中的节点数目在范围 `[0, 104]` 内
  - `1 <= Node.val <= 50`
  - `0 <= val <= 50`



### 三、代码实现

#### （1）203题

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
    ListNode* removeElements(ListNode* head, int val) {
        ListNode *myHead=new ListNode(0);			//新建一个虚拟头结点
        myHead->next=head;							//虚拟头结点的next为实际头结点
        ListNode *cur=myHead;						//当前节点
        while(cur->next!=nullptr)
        {
            if(cur->next->val==val)					//假定为要删除的值
            {
                ListNode *temp=cur->next;			//移除操作
                cur->next=temp->next;
                delete temp;
            }
            else
            {
                cur=cur->next;
            }
        }
        head=myHead->next;							//删除虚拟头结点
        delete myHead;
        return head;
    }
};
```
