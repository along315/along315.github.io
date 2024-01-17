---
title: Mac中使用brew切换python版本
date: 2024/1/11 16:15:25
tags:
    - Mac
    - brew
---

### github
https://github.com/pyenv/pyenv

### 安装
```
brew update
brew install pyenv
```

### 环境变量
```
export PYENV_ROOT=~/.pyenv
export PATH=$PYENV_ROOT/shims:$PATH
```

### pyenv基本语法
```
安装版本
pyenv install ${version}
查看所有安装的版本
pyenv versions  
全局使用该版本
pyenv global ${version}
卸载python版本
pyenv uninstall <versions>
命令参考
pyenv --help
```