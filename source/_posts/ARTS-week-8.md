---
title: ARTS挑战第8周（2019.5.13~5.19）
date: 2019-05-13
updated: 2019-05-22
categories:
- ARTS
permalink: arts-week-8
mathjax: true
---

[ARTS挑战](https://www.zhihu.com/question/301150832) 指每周完成：
* Algorithm：每周至少做一个 leetcode 的算法题
* Review：阅读并点评至少一篇英文技术文章
* Tip：学习至少一个技术技巧
* Share：分享一篇有观点和思考的技术文章（理解为输出）

# Algorithm: #19 Remove Nth Node From End of List
问题：将一个链表的倒数第n个节点删除

解答：简单的快慢指针方法，让慢指针始终落后快指针n个位置，最后删除慢指针的下一个元素

```C++
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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        int count = 0;
        ListNode* slow = head;
        ListNode* fast = head;
        while(fast->next != NULL) {
            fast = fast->next;
            ++count;
            if (count > n) {
                slow = slow->next;
            }
        }
        if (count < n-1) {
            return move(head);
        } else if (count == n-1) {
            return move(head->next);
        } else {
            slow->next = slow->next->next;
            return move(head);
        }
    }
};
```

> Runtime 4ms，超过98.68%的提交  
> Memory Usage 8.5MB，超过81.87%的提交

# Review: 《The most important skill a programmer can learn》

https://medium.freecodecamp.org/the-most-important-skill-a-programmer-can-learn-9d410c786baf

> 明白什么时候不应该写代码，可能是一个程序员最应该学习的技能 —— 《代码整洁之道》

程序员就是通过写代码来解决问题，而且程序员也热爱写代码。然而太热衷于写代码会让我们忽略其他一些重要问题：

- 代码是不是可以让其他程序员轻松看懂？
- 代码是不是被充分测试了？
- 更多代码总会带来更多软件缺陷
- 代码可能在未来触发新的bug

因此，要称为一个优秀的程序员，应当避免任何不必要的代码，知道什么时候拒绝写代码。

程序员经常想在项目里面实现所有自己觉得很酷的功能，但通常高估了这个项目究竟需要多少功能。因此，首先需要了解程序项目的意义，知道核心定义，它究竟要做什么。

当发现与软件核心目的无关的功能时，应当意识到拒绝，质疑那些功能，避免代码库无用地增长。

从工程方面来说，随着项目增长，越来越多的源文件塞满目录，各个文件中又有几百行代码，为了整理它们、弄懂它们，则需要更多目录、更多注释、更多架构，从而也需要更多程序员，最终导致做事越来越慢、沟通越来越困难。

最终，项目变得非常庞大，每次想增加一个小功能都会非常痛苦，于是开始错过交付时间节点。


# Tip: Linux中 `/dev/random` 和 `/dev/urandom` 的区别
`/dev/random` 和 `/dev/urandom` 都是Linux系统中提供随机数的伪设备，可以提供源源不断的随机字节数据流，使用方法也是相同的，读取即可。

```shell
$ cat /dev/random | od -x
0000000 3701 ac17 331b 6891 7f37 5e5c 690a e97c
0000020 0f70 eeb3 533f a69a 6e1e 1ec8 68f0 1147
0000040 54b2 1b1a 9d4c f77a ffef a22f 0282 b26c
0000060 1b62 a4b7 9624 8181 6809 4078 ebc5 7538
0000100 22c6 573a c30c a37e 52ae 989e e38c 987f
0000120 6cb5 dae4 fe96 81c5 a42e f5aa 48cb 0c8f
0000140 6a1a 1685 b30b 96ca 32fe 9e68 8d93 4596
```

```shell
$ cat /dev/urandom | od -x
0000000 d05a b86f 580a 1bc9 124f 5844 1274 4613
0000020 3f78 9ccb 53ba e9a7 5620 f92e c063 816e
0000040 571d b624 4b23 e6c7 e95d 1fa7 8602 2be4
0000060 1065 1ea9 b3f9 103e 37ac 26f8 4a26 a290
0000100 e73d e745 6cf7 655d aa07 87c3 b86a 295f
0000120 a44f a746 32ff 4132 3fc2 7eaa 2bd1 8819
```

在上述运行过程中可以发现，`/dev/random` 产生随机数的速度比较慢，速度也不均衡，经常出现大幅度的停顿，而 `/dev/urandom` 则一直可以快速产生随机数。

原理上来说，它们都是采用密码学安全伪随机数生成器（CSPRNG）来生成随机数，但有所不同的是， `/dev/random` 完全依赖系统收到的各类中断等作为熵，来生成随机数，在没有更多熵到来的时候，则被阻塞住了，而 `/dev/urandom` 在熵池被耗尽的时候，仍然通过相应算法来继续生成后续随机数，虽然说从密码学安全性上有所缺陷，但对于绝大部分情况来说，安全性足够，性能好很多。

# Share: 《程序员的数学3：线性代数》后2章

《程序员的数学3：线性代数》

第4章：从判断失控的角度来介绍特征值、对角化，以及无法对角化时的Jordan标准型；第5章：计算机中如何计算特征值

* {% post_link linear-algebra-note-3 %}
* {% post_link linear-algebra-note-4 %}