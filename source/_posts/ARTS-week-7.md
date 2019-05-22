---
title: ARTS挑战第7周（2019.5.6~5.12）
date: 2019-05-06
updated: 2019-05-22
categories:
- ARTS
permalink: arts-week-7
mathjax: true
---

[ARTS挑战](https://www.zhihu.com/question/301150832) 指每周完成：
* Algorithm：每周至少做一个 leetcode 的算法题
* Review：阅读并点评至少一篇英文技术文章
* Tip：学习至少一个技术技巧
* Share：分享一篇有观点和思考的技术文章（理解为输出）

# Algorithm: LeetCode #17 Letter Combinations of a Phone Number
问题：对于九宫格输入法，通过输入的数字，推算出所有可能的字母组合

解答：其实就是一个变种的全排列问题，可以按照数字进位的方式来说，即：先从每个位置都是最小值开始，每一轮循环相当于“+1”，过程就是从后往前找到第一个非最大值的位置，对其“+1”，并把后面的值都设为最小值。

```C++
class Solution {
public:
    vector<string> letterCombinations(string digits) {
        char int_first_char[10] = {' ',' ','a','d','g','j','m','p','t','w'};
        int is_first_char[26] = {1,0,0,1,0,0,1,0,0,1,0,0,1,0,0,1,0,0,0,1,0,0,1,0,0,0};
        char next_char[26] = {'b','c','-','e','f','-','h','i','-','k','l','-','n','o','-','q','r','s','-','u','v','-','x','y','z','-'};
        
        vector<string> result;
        int length = digits.size();
        char buffer[length+1] = {0};
        if (length == 0)
            return result;
        
        for (string::size_type i = 0; i < length; ++i) {
            buffer[i] = int_first_char[digits[i] - '0'];
        }
        
        string str(buffer);
        result.push_back(str);
        
        while (true) {
            int i = length - 1;
            while (i >= 0 && next_char[buffer[i]-'a']=='-')
                --i;
            if (i < 0)
                break;
            buffer[i] = next_char[buffer[i]-'a'];
            ++i;
            for (;i<length;++i) {
                buffer[i] = int_first_char[digits[i]-'0'];
            }
            string str(buffer);
            result.push_back(str);
        }
        return move(result);
    }
};
```

> Runtime: 4ms, 超过 95.71% 的提交  
> Memory Usage: 8.4 MB，超过 96.00% 的提交

# Review: 《The Hitchhiker’s Guide to Feature Extraction》

https://towardsdatascience.com/the-hitchhikers-guide-to-feature-extraction-b4c157e96631


这篇文章主要讲了特征提取的一些技巧，主要是怎么把现实中的特征编码成供机器学习使用的特征，提到了很多在Kaggle比赛中的技巧。

首先介绍了一个叫Featuretools的框架，它可以进行一些自动特征工程，特别适合把一些时态数据和关系型数据集转换为机器学习使用的特征矩阵。

然后举了一个关系型数据集的例子，用代码表示出来一个关系型数据集的几个表和之间的关系，而且标明其中一些字段的类型（时间、Email、地址、标记等等），然后就能自动生成出一批特征，包括数值的最大值、平均值、标准差，包括时间的年、月、日，还有各种通过关系联合的特征。

当然现实之中并没有那么简单，像类型特征就有很多种不同的特征提取方式：

- One-Hot编码，也就是一个n维长度的向量，属于哪一类，就把对应位置置为1
- 序号编码，有些特征是有顺序的，则自然按照顺序从0开始编号
- 标签编码，虽然特征本身没有顺序，但仍然按照不同的标签顺序给出编号，这在树模型之中表现良好
- 二进制编码，对不同标签顺序给出编号，将编号的二进制表示，分拆成一批0/1取值的特征
- Hash编码，即采用Hash函数对原始特征进行处理，得到结果然后One-Hot编码
- 均值编码（Target Encoding, Mean Encoding, Likelihood Encoding），针对数量非常大的类别特征，主要思想是采用变量对应的标签label的均值来作为编码，计算过程比较复杂

对数损失裁剪技术，建议将对数损失裁剪在0.05到0.95范围内。

对于经纬度特征，可以采用半正矢公式来确定在两点之间大圆上的距离，也可以采用曼哈顿距离，或者采用一点相对另外一点的方向。

自动编码机，可以挖掘一些特征的表征向量，从而作为训练特征。

针对特征还会做一些常见处理：

- 根据最大最小值归一化
- 使用标准差正规化
- 使用log对数函数处理

对于日期时间特征，可以增加一些常识信息，比如“晚上”“上周”“上个月”。

对于一些领域特征，可以根据对这个领域的了解，设置一些具有现实含义的特征。

特征可以做交叉，比如加法、减法、除法、乘法等等。

所有这些经验，都需要发挥想象力，在实践中尝试。针对不同的模型，可能需要的特征抽取方式也有所不同。

# Tip: Linux C++ 计时方式对比
### `time()` 函数
提供 UNIX 时间戳，实际精度1秒
```C++
#include <ctime>
int main(void) {
  time_t time_start = time(nullptr);
  run(1000000000);
  time_t time_end = time(nullptr);
  std::cout << "time_start " << time_start << std::endl;
  std::cout << "time_end " << time_end << std::endl;
  std::cout << "time_duration " << time_end - time_start << "s" << std::endl;
}
```
```
time_start 1558498932
time_end 1558498933
time_duration 1s
```

### `clock()` 函数
提供 CPU 时钟计时单元（clock tick）数，需要除以 `CLOCKS_PER_SEC` 当前系统内每秒时钟计时单位总次数

受到 CPU sleep 或者多线程影响，可能会非常有问题，所以尽量不用

网上资料通常说其精度在 10ms左右，但在本机测试中，能达到亚微秒级别，可能是由于glibc 2.18后底层换为了`clock_gettime`

在64位的较新Ubuntu环境中测试，`CLOCKS_PER_SEC` 为 1000000（符合POSIX标准），`clock_t` 为long长整形

```C++
#include <ctime>
int main() {
  clock_t start = clock();
  run(100);
  clock_t end = clock();
  std::cout << "sizeof(clock_t) " << sizeof(clock_t) << std::endl;
  std::cout << "CLOCKS_PER_SEC " << CLOCKS_PER_SEC << std::endl;
  std::cout << "start " << start << ", end " << end << ", diff " << (double)(end-start) / CLOCKS_PER_SEC << "s" << std::endl;
}
```
```
sizeof(clock_t) 8
CLOCKS_PER_SEC 1000000
start 444036, end 444038, diff 2e-06s
```

### `gettimeofday()` 函数
获取当前精确时间的UNIX秒数和微秒数

本机测试精度可以达到亚微秒级，相关资料表示为毫秒级

```C++
#include <sys/time.h>
int main() {
  struct timeval tv;
  struct timeval tv_end;
  gettimeofday(&tv, nullptr);
  run(1000);
  gettimeofday(&tv_end, nullptr);
  std::cout << "tv_sec: " << tv.tv_sec << std::endl;
  std::cout << "tv_usec: " << tv.tv_usec << std::endl;

  long duration = (tv_end.tv_sec - tv.tv_sec) *1000*1000 + (tv_end.tv_usec - tv.tv_usec);
  std::cout << "duration: " << duration<< "us" << std::endl;
```
```
tv_sec: 1558500953
tv_usec: 809459
duration: 2us
```

### `clock_gettime()` 函数
推荐取代 `gettimeofday()`，数值上精确到ns，从本机测试来说，精度在100ns级别没问题

其中参数 ```CLOCK_REALTIME``` 为本机时间，而 ```CLOCK_MONOTONIC``` 不受本机时间矫正影响，可以计算绝对用时
```C++
#include <ctime>
int main() {
  struct timespec t1={0,0};
  struct timespec t2={0,0};
  clock_gettime(CLOCK_MONOTONIC,&t1);
  run(100);
  clock_gettime(CLOCK_MONOTONIC,&t2);

  long long duration = (t2.tv_sec - t1.tv_sec) * 1000*1000*1000+ (t2.tv_nsec-t1.tv_nsec);
  std::cout << "duration: " << duration << "ns" << std::endl;
}
```
```
duration: 389ns
```

### ```std::chrono::system_clock``` 和 ```std::chrono::steady_clock```
这是C++11引入的时间工具，具有更好的使用体验
其中 `std::chrono::system_clock` 使用的是本机时间，而 `std::chrono::steady_clock` 不受本机时间矫正影响，可以计算绝对用时

精度方面，本机测试与 `clock_gettime()` 一致

```C++
#include <chrono>
int main() {
  auto ct = std::chrono::steady_clock::now();
  run(100);
  auto ce = std::chrono::steady_clock::now();
  auto chrono_duration = std::chrono::duration_cast<std::chrono::nanoseconds>(ce - ct);

  std::cout << "chrono: duration "  << chrono_duration.count() << "ns" << std::endl;
  std::cout << "chrono: duration "  << double(chrono_duration.count()) * std::chrono::nanoseconds::period::num / std::chrono::nanoseconds::period::den << "s" << std::endl;
}
```
```
chrono: duration 349ns
chrono: duration 3.49e-07s
```


# Share: 《程序员的数学3：线性代数》前3章

《程序员的数学3：线性代数》

第1章：矩阵、行列式与映射；第2章：秩、逆矩阵、线性方程组笔算法；第3章：计算机中采用LU分解来解决以上问题

* {% post_link linear-algebra-note-1 %}
* {% post_link linear-algebra-note-2 %}