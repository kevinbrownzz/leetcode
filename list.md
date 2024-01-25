# 160. 相交链表
简单
相关标签
相关企业
给你两个单链表的头节点 headA 和 headB ，请你找出并返回两个单链表相交的起始节点。如果两个链表不存在相交节点，返回 null 。

# 代码
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
            Set<ListNode> visited = new HashSet<ListNode>();
            ListNode temp = headA;
            while(temp != null){
                visited.add(temp);
                temp = temp.next;
            }
            temp = headB;
            while(temp != null){
                if(visited.contains(temp))   return temp;
                temp = temp.next;
            }
            return null;
    }
}
 ```

 # 206. 反转链表
给你单链表的头节点 head ，请你反转链表，并返回反转后的链表

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode pre = new ListNode(-1);
        ListNode temp = head;
        while(temp != null){
            ListNode next  = temp.next;
            temp.next=pre;
            pre = temp;
            temp = next;
        }
        return pre;
    }
}
```

# 234. 回文链表
给你一个单链表的头节点 head ，请你判断该链表是否为回文链表。如果是，返回 true ；否则，返回 false 。
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public boolean isPalindrome(ListNode head) {
        List<Integer> valuse = new ArrayList<>();
        ListNode cur = head;
        while(cur != null){
            valuse.add(cur.val);
            cur = cur.next;
        }
         int left = 0;
         int right = valuse.size()-1;
         while(left < right){
             if(!valuse.get(left).equals(valuse.get(right)))
                return false;
            left++;
            right--;
         }
         return true;
    }
}

```

# 141. 环形链表
给你一个链表的头节点 head ，判断链表中是否有环。

如果链表中有某个节点，可以通过连续跟踪 next 指针再次到达，则链表中存在环。 为了表示给定链表中的环，评测系统内部使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。注意：pos 不作为参数进行传递 。仅仅是为了标识链表的实际情况。

如果链表中存在环 ，则返回 true 。 否则，返回 false 。
```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head == null || head.next == null){
            return false;
        }
        ListNode fast = head, slow = head;
        while(fast != null && fast.next != null){
            fast = fast.next.next;
            slow = slow.next;
            if(slow == fast)
                return true;
        }
        return false;
    }
}
```

# 21. 合并两个有序链表
将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

递归也可以解

 

示例 1：


输入：l1 = [1,2,4], l2 = [1,3,4]
输出：[1,1,2,3,4,4]
示例 2：

输入：l1 = [], l2 = []
输出：[]
示例 3：

输入：l1 = [], l2 = [0]
输出：[0]

```java/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode prehead = new ListNode(-1);
        ListNode prev = prehead;
        while(list1 != null && list2 != null){
            if(list1.val < list2.val){
                prev.next = list1;
                list1 = list1.next;
            }
            else{
                prev.next = list2;
                list2 = list2.next;
            }
            prev = prev.next;
        }
        prev.next = list2 == null? list1 :list2;
        return prehead.next;


    }
}
```

# 2. 两数相加

给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummyHead = new ListNode(0); // 创建一个虚拟头节点
        ListNode p = l1, q = l2, curr = dummyHead;
        int carry = 0; // 进位

        while (p != null || q != null) {
            int x = (p != null) ? p.val : 0;
            int y = (q != null) ? q.val : 0;
            int sum = carry + x + y;
            carry = sum / 10;

            curr.next = new ListNode(sum % 10);
            curr = curr.next;

            if (p != null) p = p.next;
            if (q != null) q = q.next;
        }

        if (carry > 0) {
            curr.next = new ListNode(carry);
        }

        return dummyHead.next; // 返回虚拟头节点的下一个节点，即结果链表的头节点
    }
}

```

超时做法 链表中存储整数进行加减操作通常与我们常规计算加减法类似 低位在前反而利于加法的计算。下面这种方法一定会超时，在大数问题上存在太多转换
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverse(ListNode l){
        ListNode prehead = new ListNode (-1);
        ListNode  pre = prehead;
        while(l != null){
            ListNode next = l.next;
            l.next = pre;
            pre = l;
            l=next;
        }
        return pre;
    }
    public int listToInt(ListNode l1){
        if(l1 == null)  return 0;
        int a = 1,ans=0;
        while(l1 != null){
            ans += a * l1.val;
            a *= 10;
        }
        return ans;
    }
    public ListNode intToList(int ans){
        ListNode head = new ListNode(-1);
        ListNode prehead = head;
        int cur = 10;
        while(ans != 0){
            ListNode temp = new ListNode(ans%10);
            head.next = temp ;
            head=head.next;
            ans = ans /10;
        }
        return prehead;

    }
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        l1 = reverse(l1);l2 = reverse(l2);
        int num1,num2,ans;
        ans = listToInt(l1) + listToInt(l2);
        return intToList(ans);
    }
}
```

# 19. 删除链表的倒数第 N 个结点

提示
给你一个链表，删除链表的倒数第 n 个结点，并且返回链表的头结点。
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode prehead =new ListNode(-1);
        prehead.next = head;
        int size = 0;
        ListNode temp = prehead;
        if(head.next ==null && n==1){
            return null;
        }
        while(temp.next!= null){
            size+=1;
            temp = temp.next;
        }
        temp=prehead;
        for(int i=0;i<size-n;i++){
            temp =temp.next;
        }
        if(temp.next.next == null){
            temp.next =null;
        }
        else{
            temp.next =temp.next.next;
        }
        return prehead.next;
    }
}```