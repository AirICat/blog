---
title: github Action自动化部署hexo博客
date: 2022-08-01 13:25:31
tags: 
    - Github
    - GithubAction
    - hexo
categories:
    - [Github,Action]
---
# 前言
抱着能偷懒 就偷懒的心态研究了下GitHub Action 好家伙英文中文混合开火 直接给我干蒙了 
简单的看了下 还是成功了 后面有时间还是要了解下的 感觉很有用 *现在就是能用就行*

# 创建GitHub Action
1. 打开GitHub 仓库位置 
2. 点击 Action
3. 点击 new workflows
4. 写入 
```yml
name: deploy

on:
  push:
    branches: [ "master" ]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: latest
      - name: build
        run: npm install && npx hexo generate
      - name: deploy
        uses: peaceiris/actions-gh-pages@v3
        with: 
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_branch: gh-pages
          publish_dir: public
          cname: you.webSite.com

```

# 相关参考
[Github Actiom 市场](https://github.com/marketplace?type=actions&query=actions)
[Action nodejs-setup](https://github.com/actions/setup-node)
[Action deploy-pages](https://github.com/peaceiris/actions-gh-pages)