---
title: Hello 'Github Pages' World!
date: 2019-05-05
updated: 2019-05-05
permalink: hello-github-pages-world
mathjax: true
---

今天搭建好了Hexo博客，终于可以把先前的内容搬迁过来了

# 搭建教程

* Hexo搭建 https://thief.one/2017/03/03/Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2%E6%95%99%E7%A8%8B/
* Submodule管理Hexo主题 https://www.jianshu.com/p/5abacac4133c
* Hexo下mathjax的转义问题 https://segmentfault.com/a/1190000007261752
* Hexo 集成 Travis CI 自动部署博文 https://wafer.li/Hexo/Hexo%20%E9%9B%86%E6%88%90%20Travis%20CI%20%E8%87%AA%E5%8A%A8%E9%83%A8%E7%BD%B2%E5%8D%9A%E6%96%87/

# 搭建步骤

* Github上创建username.github.io的库，已经可以通过url访问
* 域名CNAME指向该地址
* 本地安装node.js和Hexo
* hexo创建新环境，进行各类配置
* 安装hexo主题，我选择了Hexo NexT，里面配置好MathJax支持
* hexo g & hexo d 进行推送到github
* 大功告成

# 测试代码高亮
```python
def a(b):
    a = b
    return a
```
```C++
#include<iostream>
int main(int argc,int argv[]){
 return 0;
}
```

# 测试公式显示能力

行间公式：
$$\alpha_\beta=\gamma_\delta$$
$$a*b$$
$$a**b$$
$$X \boldsymbol{X}$$

行内公式 $\alpha_\beta=\gamma_\delta$

行内公式 $a*b$

行内公式 $a**b$

测试加粗：

$$X \pmb{X} \alpha \pmb{\alpha}$$
$$X\boldsymbol{X} \alpha\boldsymbol{\alpha}$$
