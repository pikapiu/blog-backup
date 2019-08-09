---
title: git所需要的最小配置
date: 
categories: git
tags: 
 - git
 - config
thumbnail: /images/wolf.jpg
---

### git help xxx //打开本地帮助文档
```
git config --local user.name 'example'
git config --local user.email 'example@domain.com'
```

#### config的三个作用域:
git config --local   //对某个仓库有效

git config --global  //对当前用户的所有仓库有效

git config --system  //对系统的所有用户有效

#### 查看配置:

git config --list --local

 配置文件的存放目录：**./.git/config**

---
git config --list --global 

配置文件的存放目录：**user/.gitconfig**

例如：C:\Users\rice\.gitconfig



---
git config --list --system 

配置文件的存放目录：**$(prefix)/etc/gitconfig**

---
### 优先级

local > global > system