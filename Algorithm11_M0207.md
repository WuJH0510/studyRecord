# 算法学习篇（六）：链表05之链表相交

## 以leetcode面试题02-07为例

​		

### 一、算法原理

​		链表相交，首先需要知道两个链表的长度，可以通过遍历链表获得。之后假定链表A为长链表，计算两链表长度差值，让长链表的当前节点指针移动到与短链表到末尾节点距离一致的节点，保证链表剩余部分长度一致。然后两个链表的指针同时往前移动，若找到地址相同的节点（链表相交节点）则返回该节点，若到达链表末尾节点仍未找到相交节点，则返回空值。

### 二、力扣原题

#### （1）[面试题 02.07. 链表相交](https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/)

- 给你两个单链表的头节点 `headA` 和 `headB` ，请你找出并返回两个单链表相交的起始节点。如果两个链表没有交点，返回 `null` 。

  图示两个链表在节点 `c1` 开始相交**：**

  [![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_statement.png)](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_statement.png)

  题目数据 **保证** 整个链式结构中不存在环。

  **注意**，函数返回结果后，链表必须 **保持其原始结构** 。

   

  **示例 1：**

  [![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_example_1.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_1.png)

  ```
  输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
  输出：Intersected at '8'
  解释：相交节点的值为 8 （注意，如果两个链表相交则不能为 0）。
  从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。
  在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
  ```

  **示例 2：**

  [![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_example_2.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_2.png)

  ```
  输入：intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
  输出：Intersected at '2'
  解释：相交节点的值为 2 （注意，如果两个链表相交则不能为 0）。
  从各自的表头开始算起，链表 A 为 [0,9,1,2,4]，链表 B 为 [3,2,4]。
  在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。
  ```

  **示例 3：**

  [![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_example_3.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_3.png)

  ```
  输入：intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
  输出：null
  解释：从各自的表头开始算起，链表 A 为 [2,6,4]，链表 B 为 [1,5]。
  由于这两个链表不相交，所以 intersectVal 必须为 0，而 skipA 和 skipB 可以是任意值。
  这两个链表不相交，因此返回 null 。
  ```

   

  **提示：**

  - `listA` 中节点数目为 `m`
  - `listB` 中节点数目为 `n`
  - `0 <= m, n <= 3 * 104`
  - `1 <= Node.val <= 105`
  - `0 <= skipA <= m`
  - `0 <= skipB <= n`
  - 如果 `listA` 和 `listB` 没有交点，`intersectVal` 为 `0`
  - 如果 `listA` 和 `listB` 有交点，`intersectVal == listA[skipA + 1] == listB[skipB + 1]`



### 三、代码实现

#### （1）面试题02-07

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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        int lengthA=0,lengthB=0;
        ListNode *curA=headA;
        ListNode *curB=headB;
        while(curA!=NULL)			//求链表A长度
        {
            curA=curA->next;
            lengthA++;
        }
        while(curB!=NULL)			//求链表B长度
        {
            curB=curB->next;
            lengthB++;
        }
        curA=headA;					//返回链表当前指针位置
        curB=headB;
        if(lengthA<lengthB)			//规定链表A为长链表
        {
            swap(lengthA,lengthB);
            swap(curA,curB);
        }
        int gap=lengthA-lengthB;
        while(gap--)				//保证两链表到链表末尾的节点个数一致
        {
            curA=curA->next;
        }
        while(curA!=NULL)			//遍历寻找地址相同节点，若到链表末尾仍未找到则返回NULL
        {
            if(curA==curB)
            {
                return curA;
            }
            curA=curA->next;
            curB=curB->next;
        }
        return NULL;
    }
};
```
