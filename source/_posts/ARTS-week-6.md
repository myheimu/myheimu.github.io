---
title: ARTS挑战第6周（2019.4.29~5.5）
date: 2019-05-05
updated: 2019-05-06
categories:
- ARTS
permalink: arts-week-6
mathjax: true
---

[ARTS挑战](https://www.zhihu.com/question/301150832) 指每周完成：
* Algorithm：每周至少做一个 leetcode 的算法题
* Review：阅读并点评至少一篇英文技术文章
* Tip：学习至少一个技术技巧
* Share：分享一篇有观点和思考的技术文章（我理解为自己写一篇）

本周完成内容为：
<!-- toc -->

# Algorithm: LeetCode #15 3Sum
https://leetcode.com/problems/3sum/

> 问题：从一堆数字中寻找三个数能够和为0

解答：第一个坑在于元素不能重用，比如数组里只有一个-1，但已经取了这个元素，随后通过hash之类方式发现剩下还需要一个-1的时候，就需要增加额外逻辑判断是否有足够的-1可以使用

第二个坑在于tuple的重复性，比如[-1,1,0]和[1,-1,0]只能保留一个，这个可以通过最后时刻的入库对比来去重，但要想速度够快，还是得在设计的时候就充分考虑顺序，避免重复出现

第三点在于性能，最差的模拟时间复杂度是 $O(n^3)$，稍微优化的版本是遍历前两个元素，对第三个元素通过查找方式寻找（如果是hash则为$O(n^2)$，如果是二分类方法则为$O(n^2\log{n})$）。最优的方法则是对第一个元素进行遍历，然后在后面的范围内对后两个元素进行两端逼近，复杂度能够控制在 $O(n^2)$ 以内

```C++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        vector<vector<int>> results;
        int size = nums.size();
        for (int i = 0; i < size; ++i) {
            if (nums[i] > 0) break;
            int j = i+1; 
            int k = nums.size()-1;
            while (j < k) {
                int sum = nums[j]+nums[k];
                if (sum < -nums[i]) { j++; continue; }
                if (sum > -nums[i]) { k--; continue; }
                results.push_back({nums[i], nums[j], nums[k]});
                int last_j_num = nums[j];
                int last_k_num = nums[k];
                while (j+1 < nums.size() && nums[j+1] == last_j_num)
                    j++;
                while (k-1 >= 0 && nums[k-1]  == last_k_num)
                    k--;
                j++;
            }
            while (i+1 < nums.size() && nums[i] == nums[i+1])
                i++;
        }
        return move(results);
    }
};
```

运行结果：
> Runtime: 96 ms，超过98.00%的提交  
> Memory Usage: 14.7 MB，超过99.00%的提交

# Review: 《Five Machine Learning Paradoxes that will Change the Way You Think About Data》
https://towardsdatascience.com/five-machine-learning-paradoxes-that-will-change-the-way-you-think-about-data-e100be5620d7

悖论，就是针对问题的原始前提而导致了明显的自相矛盾结论。

例如**忒休斯之船悖论**：一艘船逐渐替换其中腐烂的零件，当全部零件都被更换之后，这艘船还是原来的船么？

例如**罗素悖论**：对于一条规则“自己不属于自己”而构成的集合R，如果R属于R，那么根据定义R不属于R，如果R不属于R，那么根据定义，R属于R。

机器学习中同样有一些著名的悖论：

**辛普森悖论**

“一所大学，分学院申请，一定比例通过并入学，每个学院的女性入学通过率均高于男性，但整个学校平均的女性入学通过率却高于男性”

简单的平均值没有考虑到数据集中特定集合的相关性。

所以机器学习中，针对不同数据集的无监督训练，可能在合并数据集之中产生巨大变化。

**布雷斯（Braess）悖论**
“在拥挤的交通网络中增加一条道路，反而可能增加拥堵”

在纳什均衡游戏中，当其他人都坚持使用相同策略，那么单个人没有动力应用新策略。

该悖论在自主的多智能体强化学习场景中需要考虑。

**莫拉维克（Moravec）悖论**
“与普遍的认知相反，高级推理需要的计算量低于低级无意识认知”

简单的AI就可以完成非常复杂的统计和数据任务，这些对人来说是不可能的，然而很多对于人来说微不足道的小事儿，比如用手抓住物体，却需要非常复杂的AI模型。

从迁移学习角度来看，Moravec悖论告诉我们应当在不同的机器学习模型之间推广知识。另外，机器学习可以考虑将人与算法结合。

**准确率悖论**
“准确率并不总是对模型的一个良好指标”

主要是在于数据集非常不平衡的情况下，单纯看准确率指标无法做出充分的区分。可以更加深入观察精度和召回率，并针对不同类型的问题，设置不同的指标倾向。

**可学习性-哥德尔（Learnability-Godel）悖论**
哥德尔连续统假设与机器学习的可学习性可以联系起来，机器学习的可学习性也是无法通过选择一个公理宇宙就能解决的状态。

# Tips: 使用Github Pages & Hexo搭建技术博客

{% post_link hello-github-pages-world %}


# Share: 《程序员的数学2：概率统计》读书笔记

* {% post_link probability-and-statistics-note-1 %}
* {% post_link probability-and-statistics-note-2 %}
* {% post_link probability-and-statistics-note-3 %}



