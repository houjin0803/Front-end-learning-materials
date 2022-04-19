# 一、链表

## 1、链表反转

- 链接：https://leetcode-cn.com/problems/reverse-linked-list/

- 思路

  涉及到链表的题目应该首先想到用指针来解决，本题可以使用三个指针：`pre cur next`。首先`pre`指针指向的是当前节点的前一个节点，`cur`指针指向的是当前节点，`next`指针指向的是当前节点的下一个节点。反转链表无非就是将原链表的指针反向，初始时：`cur`指向头节点，`pre`就指向`null`（头结点之前没有，就是空），`next`指向`cur`的下一个节点。然后将头结点的指针指向`pre`（这就实现了指针反转），再让`pre`指向`cur`所在的节点，而`cur`再指向下一个节点，而下一个节点的值刚好就是`next`，这也是我们为什么设`next`指针的原因，因为一旦指针反转，当前节点和后面节点就断了关联，因此通过`next`指针可以保留下一个节点的信息，循环上述过程即可反转整个链表。

- 代码

  ```js
  var reverseList = function(head) {
      var pre = null
      var cur = head
      while(cur){
         const next = cur.next
          cur.next = pre
          pre = cur
          cur = next
      }
      return pre
  };
  ```

  