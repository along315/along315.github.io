---
title: node版本切换
date: 2024/1/8 17:45:25
tags: 
    - node
---

### 场景
比如我希望将一个vue项目打包dist丢给运维发布，这个时候就会涉及到node版本切换。
node过高与过低都会导致我们打包失败。

### github
https://github.com/nvm-sh/nvm

### nvm基本语法
```
使用node版本
nvm use ${version}
查看所有安装的node
nvm ls
查看命令
nvm tab
卸载node版本
nvm uninstall ${version}
```

### 实例
```
$ nvm use 16
Now using node v16.9.1 (npm v7.21.1)
$ node -v
v16.9.1
$ nvm use 14
Now using node v14.18.0 (npm v6.14.15)
$ node -v
v14.18.0
$ nvm install 12
Now using node v12.22.6 (npm v6.14.5)
$ node -v
v12.22.6
```


