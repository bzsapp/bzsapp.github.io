---
# 文章常用yaml定义 #
layout: post                 # 调用_layouts下面的某一个模板
author: "sh"                 #文章作者      
title: Markdown and git命令基本使用测试    #文章标题
published: true              # 该文章是否需要发布
categories: ["python", "MIS","markdown"]      # 分类
tags: ["tag-1","tag-2","tag-3"]    # 标签
permalink: /:title/think-bzs       # 来定义你最终的文章链接是什么形式
date: 2018-12-30
---

正文区域：

[TOC]

## Go to the folder where you want to ##
store your project, and clone the new repository:

$$
x = \dfrac{-b \pm \sqrt{b^2 - 4ac}}{2a}
$$

使用 git clone 拷贝一个 Git 仓库到本地[^1]，让自己能够查看该项目，或者进行修改。
如果你需要与他人合作一个项目，或者想要复制一个项目，看看代码，你就可以克隆那个项目。 执行命令：
```python
# 这是一个正常使用测试实例
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(9)
y = np.sin(x)
z = np.cos(x)
```
>上善如水，厚德载物

Git 为你的每一个提交都记录你的名字与电子邮箱地址，所以第一步需要配置用户名和邮箱地址。
```
$ git config --global user.name 'runoob'
$ git config --global user.email test@runoob.commit
```
+ [x] 厚德载物
+ [ ] 上善若水
  - 厚德载物
    * 不惜名，莫嫌仇，不吝财，人皆堪用也
    * 这样，懂得为他人创造价值，人际关系才能持久，才是真正社交

## Push it ##
* Add, commit, and push your changes:
* 使用 git add 命令将所有修改的文件写入缓存区， 而执行 git commit 将缓存区内容添加到本地仓库。
* git push 将本地仓库的修改推送到远程仓库

| -f 参数    |         字体名称         |   公式   |
| --------: | :-------------------: | ---- |
| anka        |        Anka/Coder       |  a=5-1   |
| anonymous   |      Anonymous Pro      |   b=5+3  |

## 删除所以文件和文件夹 ##
```
$ git rm * -r
```

[^1]: 参考文献：shanghairef ,today china.
