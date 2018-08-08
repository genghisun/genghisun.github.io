---
title: "git稀疏检出"
category: tech
tags: git sparsecheckout staticman
---

我github上某些文件（staticman的评论文件）的名字中用了“:”这个符号，但windows上不支持包含“:”的文件名，于是乎在pull的时候就会报错`unable to create file xxx (Invalid argument)`

git目前没有 pull的时候将字符进行转换的功能，故这个问题有以下两种解决方式：
1. 在创建文件的时候避免使用 文件名中不能出现的特殊符号，如*?:等等
2. 使用git的稀疏检出(sparse checkout)功能，这个功能可以实现只读取部分目录的内容

稀疏检出(sparse checkout)具体设置方法：
1. 在.git/config文件中加入一行sparsecheckout = true，<br>或者在终端中输入命令`git config core.sparseCheckout true`
```
[core]
	sparsecheckout = true
```
2. 在.git/info/sparse-checkout文件中（不存在就创建）每行写一个匹配模式，和语法和.gitignore一样，可以使用*和!<br>需要着重说明的是，在反选（即不获取某些目录）时，第一行必须是`/*`，接下来每行以!开头，如我不获取/_data/comments/目录下的文件：
```
/*
!/_data/comments/
```
