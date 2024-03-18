# 算法学习篇（六）：链表07之设计链表

## 以leetcode707题为例

​		

### 一、算法原理

​		本题目需要设计一个链表，以设计单链表为例，在不计算虚拟头节点的情况下，下标从0开始。

​		首先需要设计链表的节点，节点需要有 **数值** 和 **下一节点next** 两个属性，并提供初始化函数（构造函数）。

​		为操作简便，链表类的构造函数需要先构造一个虚拟头节点，并初始化长度，对应的链表需要定义2个属性：**虚拟头节点**和**长度**。

### 二、力扣原题

#### （1）[707. 设计链表](https://leetcode.cn/problems/design-linked-list/)

- 你可以选择使用单链表或者双链表，设计并实现自己的链表。

  单链表中的节点应该具备两个属性：`val` 和 `next` 。`val` 是当前节点的值，`next` 是指向下一个节点的指针/引用。

  如果是双向链表，则还需要属性 `prev` 以指示链表中的上一个节点。假设链表中的所有节点下标从 **0** 开始。

  实现 `MyLinkedList` 类：

  - `MyLinkedList()` 初始化 `MyLinkedList` 对象。
  - `int get(int index)` 获取链表中下标为 `index` 的节点的值。如果下标无效，则返回 `-1` 。
  - `void addAtHead(int val)` 将一个值为 `val` 的节点插入到链表中第一个元素之前。在插入完成后，新节点会成为链表的第一个节点。
  - `void addAtTail(int val)` 将一个值为 `val` 的节点追加到链表中作为链表的最后一个元素。
  - `void addAtIndex(int index, int val)` 将一个值为 `val` 的节点插入到链表中下标为 `index` 的节点之前。如果 `index` 等于链表的长度，那么该节点会被追加到链表的末尾。如果 `index` 比长度更大，该节点将 **不会插入** 到链表中。
  - `void deleteAtIndex(int index)` 如果下标有效，则删除链表中下标为 `index` 的节点。

   

  **示例：**

  ```
  输入
  ["MyLinkedList", "addAtHead", "addAtTail", "addAtIndex", "get", "deleteAtIndex", "get"]
  [[], [1], [3], [1, 2], [1], [1], [1]]
  输出
  [null, null, null, null, 2, null, 3]
  
  解释
  MyLinkedList myLinkedList = new MyLinkedList();
  myLinkedList.addAtHead(1);
  myLinkedList.addAtTail(3);
  myLinkedList.addAtIndex(1, 2);    // 链表变为 1->2->3
  myLinkedList.get(1);              // 返回 2
  myLinkedList.deleteAtIndex(1);    // 现在，链表变为 1->3
  myLinkedList.get(1);              // 返回 3
  ```

   

  **提示：**

  - `0 <= index, val <= 1000`
  - 请不要使用内置的 LinkedList 库。
  - 调用 `get`、`addAtHead`、`addAtTail`、`addAtIndex` 和 `deleteAtIndex` 的次数不超过 `2000` 。

   



### 三、代码实现

#### （1）707题

以下是C++代码实现：

```c++
class MyLinkedList {
public:
    struct LinkListNode{
        int val;
        LinkListNode *next;
        LinkListNode(int val):val(val),next(nullptr){};
    };

    MyLinkedList() {
        myHead=new LinkListNode(0);
        length=0;
    }
    
    int get(int index) {
        if(index<0||index>=length) return -1;
        LinkListNode *temp=myHead;
        for(int i=0;i<=index;i++)
        {
            temp=temp->next;
        }
        return temp->val;
    }
    
    void addAtHead(int val) {
        LinkListNode *cur=new LinkListNode(val);
        cur->next=myHead->next;
        myHead->next=cur;
        length++;
    }
    
    void addAtTail(int val) {
        LinkListNode *cur=new LinkListNode(val);
        LinkListNode *tail=myHead;
        while(tail->next!=nullptr) tail=tail->next;
        tail->next=cur;
        cur->next=nullptr;
        length++;
    }
    
    void addAtIndex(int index, int val) {
        if(index<0||index>length) return;
        LinkListNode *temp=myHead;
        for(int i=0;i<index;i++)
        {
            temp=temp->next;
        }
        LinkListNode *cur=new LinkListNode(val);
        cur->next=temp->next;
        temp->next=cur;
        length++;
    }
    
    void deleteAtIndex(int index) {
        if(index<0||index>=length) return;
        LinkListNode *temp=myHead;
        for(int i=0;i<index;i++)
        {
            temp=temp->next;
        }
        LinkListNode *cur=temp->next;
        temp->next=cur->next;
        cur->next=nullptr;
        delete cur;
        length--;
    }

private:
    LinkListNode *myHead;
    int length;
};

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList* obj = new MyLinkedList();
 * int param_1 = obj->get(index);
 * obj->addAtHead(val);
 * obj->addAtTail(val);
 * obj->addAtIndex(index,val);
 * obj->deleteAtIndex(index);
 */
```
