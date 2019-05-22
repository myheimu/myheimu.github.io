---
title: ARTS挑战第5周（2019.4.22~28）
date: 2019-04-28
updated: 2019-05-06
categories:
- ARTS
permalink: arts-week-5
mathjax: true
---

[ARTS挑战](https://www.zhihu.com/question/301150832) 指每周完成：
* Algorithm：每周至少做一个 leetcode 的算法题
* Review：阅读并点评至少一篇英文技术文章
* Tip：学习至少一个技术技巧
* Share：分享一篇有观点和思考的技术文章（我理解为自己写一篇）

# Algorithm: LeetCode #11 Container With Most Water
https://leetcode.com/problems/container-with-most-water/

> 解答：  
> 最直接的方法就是两两比较，算法复杂度 $O(n)$。  
> 通过观察可以发现，一个“最佳结果”，其左边挡板不可能还有比它更左更高的存在，否则可以反证还有更好的最佳结果。右边也一样。  
> 所以，可以通过从左向右寻找当前最高值的方式，确定可以候选作为左挡板的位置；同理，右边也一样。

```C++
#include <stdlib.h> 
class Solution {
public:
    int maxArea(vector<int>& height) {
        int size = height.size();
        
        vector<int> right_pos;
        int right_max = height[size-1];
        right_pos.push_back(size-1);
        for (int i = size-2; i >= 0; --i) {
            if (height[i] > right_max) {
                right_pos.push_back(i);
                right_max = height[i];
            }
        }
        
        int left_max = 0;
        int max_water = 0;
        for (int i = 0; i < size; ++i) {
            if (height[i] > left_max) {
                for (auto j : right_pos) {
                    if (j > i) {
                        int sum = (j - i) * min(height[i], height[j]);
                        if (sum > max_water) {
                            max_water = sum;
                        }
                    }
                }
                left_max = height[i];
            }
        }
        return max_water;
    }
};
```

运行结果：
> Runtime: 20 ms 超过98.41%的提交  
> Memory Usage: 9.9 MB 超过92.63%的提交  

# Review: 领域驱动设计《DDD 101 — The 5-Minute Tour》
https://medium.com/the-coding-matrix/ddd-101-the-5-minute-tour-7a3037cf53b8

> 任何傻瓜都能编写计算机可以理解的代码，优秀的程序员编写人类可以理解的代码 —— 《重构》

领域驱动设计（DDD）的全部含义就是：表达一个有意义的面向对象模型，它自己就说明了它在做什么。

DDD相比标准的面向对象程序设计（OOP）有什么区别呢？答案就是：没区别。

DDD只不过是把OOP应用到了商业模型上罢了。

领域通用语言（Ubiquitous Language）

虽然之前我写代码让人满意，但代码之中总感觉出了问题，无法弄清楚。在阅读《领域驱动设计：软件核心复杂性应对之道》一书之前，我努力学习了一堆花里胡哨的设计模式。

在DDD这本书之中，想法很简单：“想知道什么是铁锹；如何使用它；它做了什么……那就问一个知道的人”

我们之中有多少开发人员，只是随便看了一眼需求，随意浏览了业务规则，然后就立即开始技术架构和编码？很多。

解决方法就是：理解它。

> 如果你无法向一个六岁孩子解释某件事，说明你自己并不了解它。——爱因斯坦

还有一个推论是：为了理解某个问题，我必须面试一个解决过这个问题的人。

在敏捷方法之中，也同样倡导随时与正确的人沟通。

当你与商人沟通，使用你的技能去帮助他解决问题、节省时间、增加品质的时候，一切变得更有意思，你不再只是为解决方案写代码，你也将称为解决方案的一部分，了解一切。

> 你应该像给第一个孩子起名字一样给变量起名字。——《Clean Code》

每个类、每个方法、每个变量都应当仔细命名，以保证他们讲述的故事正式你正在编写的商业故事。因为在将来谈论起新功能或者bug的时候，代码即对应业务。

如果有人质疑，你可以问它，以下两段代码，哪个更爱读？
```php
if ($data[$i][$j] > $x) {
   //some code here
}
```
```php
if ($activityReport[$employeeId][$month] > $salesGoal) {
   //some code here
}
```
健康检查：贫血还是充血？

“我的对象模型到底是真实的对象模型？还只是伪造的程序代码？”

于是我遭遇了贫血模型综合征。

> 贫血模型这种反模式的根本恐怖之处在于，它与面向对象设计的基本思想相违背。它只是组合数据并处理，只不过是一种程序代码设计。而很多人以为贫血对象就是真实的对象，完全忽略了面向对象的全部意义 —— Martin Fowler

为了反省自己的代码，我反问自己“可以把所有对象都换成hashmap么？”结论是肯定的。

我早就养成了数据与功能的分离习惯，这完全违背了面向对象的信条。这也是为什么我经常有几百个service操纵数据对象，还有巨大的controller来协调他们的混乱性。

DDD的经验法则：将数据和逻辑结合在一起。

以上形成了两个主要概念：与商人交谈以便代码反映他们的问题；使用真实对象建模。

但尽管如此，项目发展中还要克服两个问题：冲突和复杂性。

为了解决不同环境中类似概念的冲突问题，为了解决一个模型包括了过多的复杂智能问题，解决方案就是“有界上下文”（Bounded Contexts）。

例如Client，可以设置一堆ClientForTheLogisticTeam、ClientForTheMarketingTeam、ClientForTheAccountingTeam等，但非常容易混淆。又不能违反遵从商业业务的原则。

所以可以设置不同的有界上下文环境，系统的每一个部分都有自己的智能、数据和词汇。

DDD同样包括很多设计模式，可以使用他们来匹配商业规则，比如Entity、Value Object、Domain Service、Aggregate、Aggregate Root、Factory、Repository

总结来说，DDD就是在一个有界上下文环境内编写领域通用语言。

# Tips: $\LaTeX$ 数学公式用法
{% post_link latex-math-example %}


# Share: 《文本上的算法——深入浅出自然语言处理》读书笔记

{% post_link algorithm-for-text-note %}
