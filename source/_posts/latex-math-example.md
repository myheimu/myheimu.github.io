---
title: LaTeX数学公式入门
date: 2019-05-06
updated: 2019-05-06
categories:
- 工具
permalink: latex-math-example
mathjax: true
---

$\TeX$（读作/tɛx/，音“泰赫”） 是高德纳（Donald E. Knuth）在编纂巨著《计算机程序设计艺术》时觉得当时排版系统太难用而发明的排版系统引擎。

$\LaTeX$ 是一个宏包，用于利用预定义的页面设置

由于搭配宏包的不同，不同系统里对以下功能支持范围也有所不同。如果在页面中显示为$\unknownsomething$（红色），则说明当前系统不支持该命令。

详细内容参见 [一份不太简短的$\LaTeX2e$介绍](http://www.mohu.org/info/lshort-cn.pdf)

# 基本使用

```
单个 $ 符号代表行内公式：$a_{1}$，两个 $ 符号代码行间公式：
$$a_{1}$$
```
单个 `$` 符号代表行内公式：$a_{1}$，两个 `$` 符号代码行间公式：
$$a_{1}$$

```
$$空格：3/18小空格|\,|，4/18小空格|\:|，5/18小空格|\;|，中等空格|\ |$$
$$大空格|\quad|，大空格|\qquad|，-3/18空格a\!b$$
$$换行\\用双斜杠$$
```
$$空格：3/18小空格|\,|，4/18小空格|\:|，5/18小空格|\;|，中等空格|\ |$$
$$大空格|\quad|，大空格|\qquad|，-3/18空格a\!b$$
$$换行\\用双斜杠$$

```
$$上标\qquad a^1 a^{123} e^{a^n}$$
$$下标\qquad a_b a_{bcd} a_{b_c}$$
$$上下标\qquad a_{b}^{c}$$
```
$$上标\qquad a^1 a^{123} e^{a^n}$$
$$下标\qquad a_b a_{bcd} a_{b_c}$$
$$上下标\qquad a_{b}^{c}$$
```
$$平方根\qquad \sqrt{x} \sqrt[3]{y} \sqrt[n]{\sqrt{n}+y}$$
```
$$平方根\qquad \sqrt{x} \sqrt[3]{y} \sqrt[n]{\sqrt{n}+y}$$
```
$$上下水平线\qquad \overline{m+n} \qquad \underline{m+n}$$
```
$$上下水平线\qquad \overline{m+n} \qquad \underline{m+n}$$
```
$$上下花括号加注释\qquad \overbrace{0,0,\dots,0}^{\text{共n项}} \qquad \underbrace{0,0,\dots,0}_{\text{共n项}}$$
```
$$上下花括号加注释\qquad \overbrace{0,0,\dots,0}^{\text{共n项}} \qquad \underbrace{0,0,\dots,0}_{\text{共n项}}$$
```
$$分数\qquad \frac{1}{2+3+4^5}$$
```
$$分数\qquad \frac{1}{2+3+4^5}$$
```
$$求和 \sum_{i=1}^{n}x_i 、乘积 \prod_i{x_i}、积分\int_{-\infty}^{\infty}x$$
```
$$求和 \sum_{i=1}^{n}x_i 、乘积 \prod_i{x_i}、积分\int_{-\infty}^{\infty}x$$

# 矩阵和类似形状
```
\begin{matrix}
a&b\\
c&d\\
\end{matrix} \quad
\begin{bmatrix} a&b\\ c&d\\ \end{bmatrix} \quad
\begin{vmatrix} a&b\\ c&d\\ \end{vmatrix} \quad
\begin{pmatrix} a&b\\ c&d\\ \end{pmatrix} \quad
\begin{Bmatrix} a&b\\ c&d\\ \end{Bmatrix} \quad
\begin{Vmatrix} a&b\\ c&d\\ \end{Vmatrix}
```
$$
\begin{matrix}
a&b\\
c&d\\
\end{matrix} \quad
\begin{bmatrix} a&b\\ c&d\\ \end{bmatrix} \quad
\begin{vmatrix} a&b\\ c&d\\ \end{vmatrix} \quad
\begin{pmatrix} a&b\\ c&d\\ \end{pmatrix} \quad
\begin{Bmatrix} a&b\\ c&d\\ \end{Bmatrix} \quad
\begin{Vmatrix} a&b\\ c&d\\ \end{Vmatrix}
$$

```
$$P=\begin{pmatrix}
X_{11}&X_{12}&\cdots&X_{1n}\\
X_{21}&X_{22}&\cdots&X_{2n}\\
\vdots&\vdots&\ddots&\vdots\\
X_{m1}&X_{m2}&\cdots&X_{mn}\\
\end{pmatrix}
```
$$P=\begin{pmatrix}
X_{11}&X_{12}&\cdots&X_{1n}\\
X_{21}&X_{22}&\cdots&X_{2n}\\
\vdots&\vdots&\ddots&\vdots\\
X_{m1}&X_{m2}&\cdots&X_{mn}\\
\end{pmatrix}
$$

```
$$Y= \begin{cases}
a&if(x>0)\\
b&if(x<0)\\
0&else
\end{cases} $$
```
$$Y= \begin{cases}
a&if(x>0)\\
b&if(x<0)\\
0&else
\end{cases} $$

# 对齐
```
$$\begin{aligned}
f(x) & =  \cos(x) \\
x & =  -\sin(x+y) \\
 & =  \tan(z)+\cot(z) \\
\end{aligned}$$
```
$$\begin{aligned}
f(x) & =  \cos(x) \\
x & =  -\sin(x+y) \\
 & =  \tan(z)+\cot(z) \\
\end{aligned}$$

# 字体和大小
$$\begin{cases}
{AMO,\beta\mu,012}& 默认\\
\mathbf{AMO,\beta\mu,012}& \backslash mathbf\\
\bm{AMO,\beta\mu,012}&\backslash bm（需bm支持）\\
\boldsymbol{AMO,\beta\mu,012} &\backslash boldsymbol（需asmmath支持）\\
\pmb{AMO,\beta\mu,012} &\backslash pmb（需asmmath支持）\\
\end{cases}$$

$$\begin{cases}
{AMO,\beta\mu,012}& 默认\\
\mathrm{AMO,\beta\mu,012}&\backslash mathrm\\
\mathbf{AMO,\beta\mu,012}& \backslash mathbf\\
\mathsf{AMO,\beta\mu,012}& \backslash mathsf\\
\mathtt{AMO,\beta\mu,012}& \backslash mathtt\\
\mathit{AMO,\beta\mu,012}& \backslash mathit\\
\mathnormal{AMO,\beta\mu,012}& \backslash mathnormal\\
\end{cases}$$

$$\begin{cases}
ABCdef\alpha\mu 123&默认\\
\mathcal{ABCdef\alpha\mu 123}&\backslash mathcal\\
\mathscr{ABCdef\alpha\mu 123}&\backslash mathscr\\
\mathfrak{ABCdef\alpha\mu 123}&\backslash mathfrak（需eufrak支持）\\
\mathbb{ABCdef\alpha\mu 123}&\backslash mathbb（需amsfonts或asmsymb）\\
\end{cases}$$

# 重音
$$ \begin{array}{cccc}
\acute{A}&\backslash acute&
\bar{A}&\backslash bar&
\breve{A}&\backslash breve&
\check{A}&\backslash check&\\
\dot{A}&\backslash dot&
\ddot{A}&\backslash ddot&
\hat{A}&\backslash hat&
\grave{A}&\backslash grave&\\
\mathring{A}&\backslash mathring&
\tilde{A}&\backslash tilde&
\vec{A}&\backslash vec&\\
\widehat{A}&\backslash widehat&
\widetilde{A}&\backslash widetilde&
\end{array} $$

# 各类字符（略）

## 希腊字母（大小写）

## 二元关系符

## 二元运算符

## 大尺寸运算符

## 箭头

## 定界符、大尺寸定界符

## AMS 各类扩展符号