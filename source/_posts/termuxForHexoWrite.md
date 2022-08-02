---
title: 利用termux写hexo博客 
date: 2022-08-02 16:05:51
tags:
  - hexo
  - termux
categories:
  - [Adroid,termux]
---
# 前言
由于不可抗力因素 使得我有时不能使用电脑
于是我想要不用手机搭出一个hexo环境

# 解释 
1. 为什么用proot容器 而不是 termux直接运行
因为容器能隔离.... 好吧是我当时遇到了bug所以想用容器试
> 然后弄着弄着就知道怎么解决了也懒得再试一次
2. 在termux下使用什么编写博客呢？
本文由于我要学下*vim/neovim*  所以用的neovim编写

不过如果你不喜欢这样，推荐你使用 `termux-setup-storage` 将blog目录放置在可访问的储存中 供其他编辑器访问

# 配置运行环境
```bash
pkg install proot-distro
# 安装容器

proot-distro install debian
# 选择Debian容器安装

proot-distro login debian
#登入Debian容器

apt update
#更新软件列表

apt install git nodejs yarnpkg neovim
#如果你不需要neovim 可以不安装
```

这有比较坑的点 
1. 这个容器nodejs版本低 但达到 hexo推荐的 v12
2. 它不自带npm 还是怎么的 我去直接懵了 看看node-npm 看看yarnpkg (apt search到的) 选择了yarn 也就是yarnpkg

# git 初始化仓库
1. 如果你是第一次创建hexo 博客
请参看hexo文档 **现在没时间后面再补**
2. 如果你已有仓库在GitHub
```bash
git config -global user.name "youname"
git config -global user.email "youemail"
#将youname换成你想要在提交时的名字 youemail同理
```
```bash
ssh-keygen -C "写入备注"
```
此时会让你选择保存路径 就选择默认的目录
后面它会让你输入一个密码 这个密码将在你push时需要输入验证不需要就回车省略
```bash
git clone git@github.com:youname/yourepo.git
# 将 youname 换成 你的名字 yourepo 换成你的仓库名

```
如果你用的不是这个（ssh）而是http ，那验证的就是账号密码而不是ssh密钥了
对了先clone再操作不然你先init后面文件pull不下来改什么东西麻烦死了

# Hexo 使用
```bash
cd yourepo
#进入你的仓库

yarnpkg 
#补全 node_models

yarnpkg hexo 
#是否能正常使用 hexo
```

# 优化 命令唤出
在 termux用户目录下（~）编辑.bashrc 加入
```bash
alias debian='proot-distro login debian'
```
