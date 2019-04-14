## Algorithm
### 题目描述
&emsp;&emsp;给出两个**非空**的链表用来表示两个非负的整数。其中，它们各自的位数是按照**逆序**的方式存储的，并且它们的每个节点只能存储**一位**数字。  
　　如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。  
　　您可以假设除了数字 0 之外，这两个数都不会以 0 开头。  

**示例:**
> 输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)  
> 输出：7 -> 0 -> 8  
> 原因：342 + 465 = 807  

### 解题思路
**题目理解**
* 非空非负，即，至少有一位，且是正整数，符合十进位制；
* 逆序，即，按照从低位到高位(个、十、白...)排列；  

**难点**  
* 十进位制的处理。申请两个指针，一个指向当前处理后的位，一个指向下一个即将要处理的位，如果出现进位，则下一个即将要处理的位初始值赋值为1；
* 循环结束逻辑判断。两个待处理的输入链表，长度可能不一；为避免出现短的链表处理完之后有进位的情况，以及简化逻辑，直接将短的链表高位补0处理。

### 实现(java)
```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode retNode = new ListNode(-1);
        ListNode currNode = retNode, nextNode = retNode;
        boolean isDecadeCarry = false, isL1End = false, isL2End = false;
        do {
            int val = (nextNode == null || nextNode.val < 0) ? l1.val + l2.val : l1.val + l2.val + nextNode.val;
            if (val >= 10) {
                isDecadeCarry = true;
                val -= 10;
            }

            if (null == nextNode) {
                currNode.next = nextNode = new ListNode(val);
            } else {
                nextNode.val = val;
            }

            if (isDecadeCarry) {
                nextNode.next = new ListNode(1);
            }

            currNode = nextNode;
            nextNode = nextNode.next;
            l1 = l1.next;
            if(null == l1) isL1End = true;
            l2 = l2.next;
            if(null == l2) isL2End = true;
            if(isL1End && isL2End){
                break;
            }else if(isL1End){
                l1 = new ListNode(0);
            }else if(isL2End){
                l2 = new ListNode(0);
            }

            isDecadeCarry = false;
        } while (l1 != null && l2 != null);

        return retNode;
    }
}
```
## Review
&emsp;&emsp;本次学习和翻译的是Android官网关于Web内容的开发指南。
* [原文地址](https://developer.android.google.cn/guide/webapps)
* [翻译地址](https://www.jianshu.com/p/45e5cd2d4baa)

## Tip
&emsp;&emsp;如何查看win10系统的具体版本号？  
　　cmd窗口输入"winver"，确定后看到具体版本号(比如，"版本1803(OS 内部版本 17134.706)")。  

**具体版本号与系统代号的对应关系：**
> 1507(10240):Windows 10 RTM，th1，即Windows 10的第一个版本。目前已停止支持，无法获得最新安全更新。长期服务版2015版除外。  
> 1511(10586):Windows 10 11月更新版，th2，目前已停止支持，无法获得最新安全更新。  
> 1607(14393):Windows 10 周年更新版，rs1(红石1)目前已停止支持，无法获得最新安全更新。长期服务版2016版除外。  
> 1703(15063):Windows 10创意者更新版。rs2(红石2)。  
> 1709(16299):Windows 10秋季创意者更新版。rs3(红石3)。  
> 1803(17134):Windows 10春季创意者更新版。rs4(红石4)。目前的最新版本。

## Share
&emsp;&emsp;明日继续
