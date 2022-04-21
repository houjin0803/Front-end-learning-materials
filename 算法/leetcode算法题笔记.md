# 一、链表

什么是链表？链表就是通过指针将节点连接在一起的线性结构。每一个节点由两部分组成：数据域和指针域（存放下一个节点的指针），最后一个指针指向null（空指针的意思），如下所示：

![image-20220420104446719](G:\typora插入图片\image-20220420104446719.png)

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


## 2、环形链表

- 链接：https://leetcode-cn.com/problems/linked-list-cycle/

- 思路

  本题还是使用指针来完成，这题要求看链表中是否存在环，这里可以使用快慢指针。这里可以用生活中的一个例子来解释：操场上跑步，操场是一个环，A和B两个人。一个人速度快，一个人速度慢，那么他们从同一起点开始跑，那么肯定存在某一时刻，他们相遇。这里一样，假设慢指针每次移动一个距离，快指针每次移动两个距离，那么如果存在环的话，他们一定会相遇。如果说不存在环，那么快指针一定先到达链表的尾端，也就是null。

- 代码

  ```js
  var hasCycle = function(head) {
      //使用快慢指针，快指针每次移动一个，慢指针每次移动两位，如果存在环，那么慢指针肯定会和快指针相遇
      if(head === null){
          return false
      }
      let slow = head
      let fast = head
      while(fast.next && fast.next.next){ //注意循环的条件，两个缺一不可。
          slow = slow.next
          fast = fast.next.next
          if(slow == fast){
              return true
          }
      }
      return false
  };
  ```


## 3、链表中第K个节点

- 链接：https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/

- 思路

  本题有两个思路，第一个是顺序查找法，第二个是双指针法

  - 顺序查找法：顺序查找法的思路应该很容易想到，即先求出链表的长度len，然后再找出第n-k个节点即可。
  - 双指针法：可以设置两个指针，一个慢指针，指向头节点，一个快指针指向第k+1个节点，这样的话快慢指针的距离就是K了，那么他们两同时移动，当快指针移动到尾部null的地方时，慢指针就移动到了倒数第k个节点。

- 代码

  ```js
  //顺序查找法
  function getKthFromEnd(head,k){
      let len = 0
      let p = head
      //首先循环链表求链表的长度
      while(p){
          len++
          p = p.next
      }
      let q = head
      //循环链表 同时长度递减，直到长度等于k
      while(len){
          if(len === k){
              return q
          }
          q = q.next
          len--
      }
  }
  //双指针
  function getKthFromEnd(head,k){
      let slow = head
      let fast = head
      //将快指针指向第k+1个节点
      for(let i=0;i<k;i++){
          fast = fast.next
      }
      //同时移动快慢指针 直到快指针移动到null
      while(fast){
          fast = fast.next
          slow = slow.next
      }
      return slow
  }
  ```

  