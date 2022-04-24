# 排序算法

## 1、冒泡排序

- 冒泡排序原理

  假设数组有`n`个数，将数组里面的数按照从小到大的顺序进行排列，那么按照冒泡排序的原理：从第一个数开始进行**相邻**的两个数的比较，左边的数比右边的数大的话，就将左边的数右移，然后又接着比较下面两个相邻的数，重复此步骤，那么经过第一趟排序，就会将最大的数放在最后，第二趟将倒数第二大的数归位，以此类推。**如果有`n`个数，就会进行`n-1`趟排序**。可以看如下动态图：

<img src="https://img-blog.csdnimg.cn/20210611113132421.gif#pic_center" alt="img"  />

- 代码

  ```js
  function bubble(a){
      let len = a.length
      //第一层for循环是需要的趟数
      for(let i=0;i<len-1;i++){
          //第二层for循环是 每一趟需要交换相邻的元素
          for(let j=0;j<len-1-i;j++){
              if(a[j]>a[j+1]){
              	[a[j],a[j+1]]=[a[j+1],a[j]]                
              }
          }
      }
  }
  ```

- 改进1

  假设在进行第三轮的时候发现数组已经是有序了，此时已经没有必要再进行下一趟的循环了，所以我们可以设置一个布尔变量`isSorted`。每一趟设置初始值为`true`，如果有元素交互则设置为`false`，当第二个for循环结束后，如果`isSorted`为true，代表本趟没有交换元素，说明数组已经有序了，可以跳出第一层for循环。代码如下：

  ```js
  function bubble(a){
      let len = a.length
      for(let i=0;i<len-1;i++){
          let isSorted = true
          for(let j=0;j<len-1-i;j++){
              if(a[j]>a[j+1]){
                  [a[j],a[j+1]] = [a[j+1],a[j]]
                  isSorted = false
              }
          }
          if(isSorted){
              break;
          }
      }
  }
  ```

- 改进2

  假设数组前半部分无序，后半部分有序比如`[3,4,2,1,5,6,7,8]`。这种情况和上面一种是不一样的，这种情况每一轮都有数据进行移动，此时我们可以在每一轮排序的最后，记录一下最后一次元素交互的位置，那么这个位置就是无序数组的边界，再往后就是有序区。

  ```js
  function bubble(a){
      let len = a.length
      //记录最后
      let lastExchangeIndex  = 0
      let sortBorder = len-1
      for(let i=0;i<lastExchangeIndex;i++){
          let isSorted = true
          for(let j=0;j<sortBorder;j++){
              if(a[j]>a[j+1]){
                  [a[j],a[j+1]] = [a[j+1],a[j]]
                  isSorted = false
                  lastExchangeIndex = j
              }
          }
          sortBorder = lastExchangeIndex
          if(isSorted){
              break;
          }
      }
  }
  ```

- 时间复杂度

  冒泡排序的时间复杂度为$O(n^2)$，是一种稳定排序，因为在两个数交换的时候，如果两个数相同，那么它们并不会因为算法中哪条语句相互交换位置。

## 2、快速排序

- 快速排序思想

  1）选择一个基准元素Pivot，一般是选择数组的第一个元素

  2）将大于Pivot的数字放在Pivot的右边

  3）将小于Pivot的数字放在Pivot左边

  4）分别对左右子序列重复以上步骤

- 具体做法

  1）选取数组的第一个元素作为基准元素Pivot

  2）建立两端的指针，左侧的指针指向数组的第一个元素，右侧的指针指向数组的最后一个元素

  3）右侧指针的当前值和Pivot进行比较，如果小于Pivot的值，则将右侧指针对应的值赋值给左侧指针指向的值；否则右侧指针一直往左移动

  4）左侧指针的当前值和Pivot进行比较，如果大于Pivot的值，则将左侧指针对应的值赋值给右侧指针指向的值，否则左侧指针一直往右移动

  5）当两个指针相遇时，说明本轮比较结束，将基准元素Pivot赋值给当前指针指向的位置。

- 代码

  ```js
  function quickSort(a,begin,end){
      if(begin>end){
          return
      }
      let left = begin
      let right = end
      let pivot = a[left]
      while(left<right){
          while(a[right] > pivot && left < right){
              right--
          }
          a[left] = a[right]
          while(a[left]<pivot && left < right){
              left++
          }
          a[right] = a[left]
      }
      a[left] = pivot
      quickSort(a,begin,left-1)
      quickSort(a,right+1,end)
  }
  ```

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

  ## 4、相交链表

- 链接：https://leetcode-cn.com/problems/intersection-of-two-linked-lists/submissions/

- 思路

  本题的一个思路就是先求出链表A和链表B的长度，假设为`lenA、lenB` ,为后面的处理起来方便，我们始终让A的长度大于B的，即lenA>lenB。如果lenA<lenB，那么就交换A、B两个链表，同时长度也进行交换。然后计算A和B长度的差值，让指向A链表的指针向前移动差值这个距离，如下所示。然后让curA和curB同时往后移动，如果两个指针相等，则直接返回当前这个指针。如果不相等，一直往后移动，移动到链表结尾还没有找到相等的，则说明两个链表没有相交的节点，返回`null

  ![img](https://code-thinking.cdn.bcebos.com/pics/%E9%9D%A2%E8%AF%95%E9%A2%9802.07.%E9%93%BE%E8%A1%A8%E7%9B%B8%E4%BA%A4_2.png)

- 代码

  ```js
  var getNodeLength(head){
      let len = 0
      let cur = head
      while(cur){
          cur = cur.next
          len++
      }
      return len
  }
  var getIntersectionNode =function(headA,headB){
      let curA = headA
      let curB = headB
      let lenA = getNodeLength(headA)
      let lenB = getNodeLength(headB)
      if(lenA < lenB){
          [lenA,lenB] = [lenB,lenA];
          [headA,headB] = [headB,headA]
      }
      let i = lenA-lenB
      while(i){
          curA = curA.next
          i--
      }
      while(curA){
          if(curA === curB){
              return curA
          }
          curA = curA.next
          curB = curB.next
      }
      return null
  }
  ```


## 4、链表的中间节点

- 链接：https://leetcode-cn.com/problems/middle-of-the-linked-list/

- 思路

  **单指针法**：先求出链表的长度len，如果len是奇数的话，直接取`len/2`的整数部分加上1，如果len是偶数的话，取`len/2 +1`，然后用p指针指向头结点，遍历链表，直到遍历到中间的节点为止。

  **双指针法**：设置快慢指针slow和fast，慢指针每次移动一个距离，快指针每次移动两个距离，当快指针移动到null的位置时，慢指针就移动到了中间节点。

- 代码

  ```js
  //单指针法
  function getListLength(head){
      let len =0
      let cur =head
      while(cur){
          cur = cur.next
          len++
      }
      return len
  }
  function middleNode(head){
      let len = getListLength(head)
      let i = Math.floor(len/2)+1
      let cur = head
      for(let j=0;j<i;j++){
          cur = cur.next
      }
      return cur
  }
  //双指针法
  function middleNode(head){
      let slow = head
      let fast = head
      while(fast && fast.next){
          fast = fast.next.next
          slow = slow.next
      }
      return slow
  }
  ```

  ## 

## 5、回文链表

- 链接：https://leetcode-cn.com/problems/palindrome-linked-list/

- 思路

  **将链表中的值复制到数组中去，然后通过数组进行判断**：通过遍历链表，将当前节点的数值存放在数组a中去，然后确定a是否是会问，这里可以使用双指针，一个指针从起点开始往中间移动，另一个指针从终点开始向中间移动，看头尾指针指向的数是否相等，只要不相等，就返会false，当首位指针相遇，结束遍历，此时说明数组中的数是会问的，返回true。

- 代码

  ```js
  //将链表中的值复制到数组中去，然后通过数组进行判断
  function isPalindrome(head){
      let a = []
      let cur = head
      while(cur){
          a.push(cur.val)
          cur  = cur.next
      }
      for(let i=0,j =a.length-1;i<=j;i++,j--){
          fi(a[i] !== a[j]){
              return false
          }
      }
      return true
  }
  ```

## 6、删除链表中的倒数第N个结点

- 链接：https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/

- 思路

  其实这道题和查找链表中的第K个节点很像 ，查找链表中的第K个节点，是需要找到第K个节点，而删除第K个节点是需要找到倒数第K+1个节点，然后将此节点的指针指向下个节点的指针所指向的节点即可。因此，我们只需要找到倒数第K+1个节点，我么可以创建一个虚拟头结点，然后让fast和slow指针指向虚拟头结点，接着让fast先前走n+1步，因为只有当fast向前走n+1步的时候，fast和slow之间的距离才是n+1，然后当fast移动到null的时候，slow就会移动到删除节点的上一个节点。如下所示：假设删除倒数第2个节点，那么当fast移动到链表的尾部时，slow就移动到了第二个节点，也就是删除节点的上一个节点，此时只需要将第二个节点指针指向第4个节点即可。

  ![img](https://code-thinking.cdn.bcebos.com/pics/19.%E5%88%A0%E9%99%A4%E9%93%BE%E8%A1%A8%E7%9A%84%E5%80%92%E6%95%B0%E7%AC%ACN%E4%B8%AA%E8%8A%82%E7%82%B91.png)

- 代码

  ```js
  /*
   * Definition for singly-linked list.
   * function ListNode(val, next) {
   *     this.val = (val===undefined ? 0 : val)
   *     this.next = (next===undefined ? null : next)
   * }
   */
  
  function removeNthFromEnd(head,n){
      let ret = new ListNode(0,head)
      let slow = ret
      let fast = ret
      for(i=0;i<n;i++){
          fast = fast.next
      }
      while(fast.next){
          fast = fast.next
          slow = slow.next
      }
      slow.next =slow.next.next
      return ret.next
  }
  ```

  