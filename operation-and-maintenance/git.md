# Git

#### 1. 安装

```bash
sudo apt-get update
sudo apt-get install git
```

#### 2. 配置

```bash
touch ~/.gitconfig
```

```ini
[user]
    email = yingzhor@gmail.com
    name = Bill Ying
[core]
    autocrlf = input
    editor = vim
[push]
    default = simple
[color]
    ui = auto
[alias]
    co = checkout
    st = status
    br = branch
    last = log -l
    ci = commit
    p = push
    m = merge
    unstage = reset HEAD
    lg = log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit
```
