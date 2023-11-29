---
layout: "post"
title: "数据结构与算法基础"
date: "2020-08-18 15:47"
categories: algorithm
tags: [Computer Language, algorithm, basic]
---

# 复杂度、对数器、二分法、异或运算
常见的评估算法优劣的核心指标：
- 时间复杂度(流程决定)
- 额外空间复杂度(流程决定)
- 常数项时间(实现细节决定)

## 基本步骤
什么是常数时间的操作？
如果一个操作的执行时间不以具体样本量为转移，每次执行时间都是固定时间，这样的操作被称为常数时间的操作。

常见的常数时间操作：
- 算数运算(+ - * % /)等
- 常见的位运算(>> >>> << | & ^)等
- 赋值、比较、自增、自减操作
- 数组寻址操作

**执行时间固定的操作都是常数时间的操作，执行时间不固定的操作，都不是常数时间的操作**

> JAVA中LinkedList的get(i)就不是常数时间的操作

如何确定算法流程的总操作数量与样本数量之间的表达式关系？
1. 想象该算法流程所处理的数据状况，要按照最差情况来
2. 把整个流程彻底拆分为一个个基本动作，保证**每个动作都是常数时间的操作**
3. 如果数据为N,看看基本动作的数量和N是什么关系

如何确定算法流程的时间复杂度？
当完成了表达式的建立，只要把最高阶项留下即可。低阶项都去掉，高阶项的系数也去掉。
记为O(忽略掉系数的高阶项)

## 时间复杂度
时间复杂度就是来衡量在整个流程中发生了多少次的常数操作这件事.

时间复杂度的意义：
当我们要处理的样本很大很大时，我们会发现低阶项是什么不是最重要的；每一项的系数是什么，不是最重要的；真正重要的是最高阶项

时间复杂度是衡量算法流程的复杂度的一种指标，该指标只与数据量有关，与过程之外的优化无关

常见的时间复杂度排序(从好到差): O(1) > O(logN) > O(N) > O(N*logN) > O(N²)  O(N³)... O(N^k) > O(2^N) O(3^N)... O(k^N) > O(N!)

## 基本排序
- 选择排序O(n²)： 轮询数组，将最小的数放到最前面
- 冒泡排序O(n²)： 数组之间两两元素顺序交换，大的值放后面
- 插入排序：将i位置上的数与前面的数相比较，只要前面的数比它大，就交换

注：
- 算法的过程和具体的语言无关
- 想分析一个算法流程的时间复杂度的前提，是对该流程非常熟悉
- 一定要确保在拆分算法的流程时，拆分出来的所有行为都是常数时间的操作。这意味着你写算法时，对自己用过的每一个系统api都是非常熟悉，否则会影响你对时间复杂度的估算

## 额外空间复杂度
实现算法流程的过程中，你需要开辟一些新的空间来支持你的算法流程

作为输入参数的空间，不算额外空间
作为输出结果的空间，不算额外空间

因为输入参数和输出结果都是必要的、和现实目标有关的，所以都不算额外空间

除上述以外，你的流程中如果还需要开辟空间才能继续下去，这部分的空间就是额外空间

如果你的流程只需要开辟有限几个变量，额外空间复杂度就是O(1)

## 常数项时间
时间复杂度这个指标是忽略低阶项和所有常数系数的。
但同样的时间复杂度的流程，运行时实际也并不是一样好。
时间复杂度只是一个重要指标，如果两个时间复杂度一样的算法还要咋时间上拼优劣，就进入到拼常数时间的阶段，简称拼常数项。

两个流程的常数项时间进行比拼不采用理论分析，直接生成随机数据测试

## 最优解
一般情况下认为，解决一个问题的算法流程，在时间复杂度的指标上，一定要尽可能的低，先满足了时间复杂度最低这个指标之后，使用最少的空间的算法流程，叫这个问题的最优解

一般最优解都是忽略掉常数项的，因为常数项这个因素只决定了实现层次的优化和考虑，和怎么解决整个问题的思想无关。

## 对数器
1. 你想要测的方法a
2. 实现复杂度不好，但是容易实现的方法b
3. 实现一个随机样本产生器
4. 把方法a和方法b跑相同的随机样本，看看得到的结果是否一样
5. 如果有一个随机样本使得比对结果不一致，打印样本进行人工干预，改对方法a和方法b
6. 当样本数量很多时，比对测试依然正确，可以确定方法a已经正确
 
## 二分法

> 算术运算怎么转换成位运算？

- 在一个有序数组中，找某个数是否存在
- 在一个有序数组中，找>=某个数最左侧的位置
- 在一个有序数组中，找<=某个数最右侧的位置
- 局部最小值问题

## 异或运算
异或运算： 相同为0，不同为1
同或运算： 相同为1，不同为0

异或运算其实就是无进位的相加，即产生了进位则忽略成0

异或运算的性质:
1. 0 ^ N == N  N ^ N == 0
2. 异或运算满足交换律和结合律

### 异或运算的应用
1. 如何不用额外变量交换两个数？
	int a = m;
	int b = n;
	a = a ^ b;
	b = a ^ b;
	a = a ^ b;
	
	最终结果： a = n; b = m;
	
	以上的交换只能a b的值为两个不同的内存空间才能操作，若a=b=arr[i]则不能用以上方法，因此实际使用时还是使用临时变量temp进行交换
	
2. 一个数组中有一种数出现了奇数次，其他都出现了偶数次，怎么找到并打印这种数？
	```java
		int eor = 0;
		for(int i = 0; i < arr.length; i++) {
			eor = eor ^ arr[i];
		}
		
	```
	以上代码运行出来最终得到的eor的值就是出现了奇数次的数

3. 如何把一个int类型的数提取出最右侧的1来？
	
	例如：int N = 00...1101010000
	
	将最右侧的1提取出来的结果是：00...0000010000
	
	N & ((~N) + 1)
	
	先将N取反，取反后的值+1，最后将这个值与N进行与运算得到的结果就是只保留最右侧的1其他位为0

4. 一个数组中有两种数出现了奇数次，其他都出现了偶数次，怎么找到并打印这两种数？
	
	```java
	
		// 使用eor=0将所有数都^一遍，最终得到的结果 eor = a ^ b
		// 且eor != 0,表示eor必然有一个位置上是1
		int eor = 0;
		for(int i = 0; i < arr.length; i++) {
			eor ^= arr[i];
		}
		
		// 提取eor中最右侧的1
		int rightOne = eor ^ ((~eor) + 1);
		
		// 定义一个新的变量onlyOne=0,将所有与eor最右侧是1同类的数进行操作
		int onlyOne = 0;
		for(int i = 0; i < arr.length; i++) {
			if((arr[i] & rightOne) != 0) {
				// (arr[i] & rightOne) != 0表示arr[i]在rightOne中为1的位数上也是1
				onlyOne ^= arr[i];
			}
		}
		
		// 以上得到的onlyOne的结果是a或者b
		// 出现奇数次的两个数a b 分别是 onlyOne和 eor^onlyOne
	```

# 链表结构、栈、队列、递归行为、哈希表
## 链表结构

- 单向链表节点结构(可以实现成范型)

    ```java

    public class Node {
        public int value;
        public Node next;

        public Node(int data) {
            value = data;
        }
    }

    ```

- 双向链表节点结构
  
  ```java
  public class DoubleNode {
      public int value;
      public DoubleNode last;
      public DoubleNode next;

      public DoubleNode(int data) {
          value = data;
      }
  }

  ```

### 单向链表和双向链表最简单的练习

  - 单链表和双链表如何反转

    ```java
    public class Code_ReverseList {
        /* 单向链表单反转 */
        // 1. 定义单向链表
        class Node {
            public int value;
            public Node next;

            public Node(int data) {
                value = date;
            }
        }

        // 2. 反转单向链表
        public Node reverseLinkedList(Node head) {
            Node pre = null;
            Node next = null;

            while(head != null) {
                next = head.next;
                head.next = pre;
                pre = head;
                head = next;
            }
        }

        /*双向链表反转*/
        // 1. 定义双向链表
        class DoubleNode {
            public int value;
            public DoubleNode last;
            public DoubleNode next;

            public DoubleNode(int data) {
                value = data;
            }
        }

        // 2. 反转双向链表
        public DoubleNode reverseDoubleList(DoubleNode head) {
            DoubleNode pre = null;
            DoubleNode next = null;
            while(head != null) {
                next = head.next;
                head.next = pre;
                head.last = next;
                pre = head;
                head = next;
            }
            return pre;
        }
    }


    ```

- 删除给定值
  
  ```java
    /**
    * 指定删除head中值为num的节点
    */
  public Node removeValue(Node head, int num) {
      // 首次遍历，过滤头节点为num的情况
      // 找到第一个不需要删的位置
      while(head != null) {
          if(head.value != num) {
              break;
          }else {
              head = head.next;
          }
      }

      Node pre = head;
      Node cur = head;

      while(cur != null) {
          if(cur.value == num) {
              // 当前值为num,将当前值的下一位赋于pre.next
              pre.next = cur.next;
          }else {
              // 当前值保留,记录当前值
              pre = cur;
          }
          cur = cur.next;
      }
      return head;
  }

  ```

## 栈和队列

### 逻辑概念

- 栈： 先进后出
  
- 堆： 先进先出
  
### 实际实现
  
- 双向链表实现
  
- 数组实现

### 常见面试题

1. 怎么用数组实现不超过固定大小的队列和栈
   
   栈： 正常使用

   队列： 环形数组

2. 实现一个特殊的栈，在基本功能的基础上再实现返回栈中最小元素的功能





 