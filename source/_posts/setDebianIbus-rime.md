---
title: 设置Debian系统的Ibus-rime
date: 2022-07-30 14:50:48
tags: 
---
# 关于
由于我*心血来潮*想在Linux桌面上建立适合我的桌面 ，所以记录一下我踩的**坑**

> 为啥用ibus呢？ 这玩意好像没有Fcitx5好用 
> 可是gnome 下系统默认输入法 和 组件是ibus 悲
> 为了整体美观 开干

# 安装 ibus-rime
```bash
sudo apt install ibus-rime
```

# 设置 ibus-rime
## *注* 环境为 gnome  桌面环境下
```bash
vi ~/.xinputrc
```
写入 
`run_im ibus`
vi操作 `i` `esc` `:wq`

后退出登录（注销）再进入
> 这个是命令操作 不过我一开始是弄得 gnome应用 里的 那个`输入法` 你可能会问我为什么一开始不说那个 因为*水水水*

# 启用 ibus-rime
1. 打开设置
2. 找到区域和语言
3. 添加输入源 `中国（汉语）` `rime`
4. 随便打开一个输入栏 切换 `中文rime` 
5. 注销登录
6. 看能不能输入中文

# 关于上述完成后打不出中文解决方案一
> 缘由 在试了半天后逛逛应用商店 发现一个ibus首选项的东西
1. 打开终端
    输入 `ibus-setup`
    在窗口中 点击输入法
    添加 `...` `中文` `rime`
    删除其他的输入法
    注销登录

再试试能不能输入中文

# 大坑
由于rime竖向向太丑于是想调成横向
官方给的
```bash
# weasel.custom.yaml
patch:
  style/horizontal: true      # 候選橫排
  style/inline_preedit: true  # 內嵌編碼（僅支持TSF）
  style/display_tray_icon: true  # 顯示托盤圖標

#ibus用户： ibus_rime.custom.yaml
```
结果您猜怎么样 **根本用不了**
解决 由于配置最后是在build中执行的 所以把文件放入build中
```bash
# ~/.config/ibus/rime/build/ibus_rime.yaml
style:
    horizontal: true
```

# 更多
[rime](https://rime.im/)
