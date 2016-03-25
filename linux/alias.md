# alias


#### 1. alias命令

* 功能: 显示定义的alias
* 用法: `$ alias`

#### 2. 常用alias

如: `~yingzhuo/.bash_alias`

```bash
###############################################################################
# 功能: 定义常用alias
# 作者: 应卓
# 日期: 2016-03-17
###############################################################################

alias cls='clear'

alias vi='vim'
alias edit='vim'
alias vir='vim -R'
alias svi='sudo vim'

alias cd..='cd ..'
alias ..='cd ..'
alias ...='cd ../../../'
alias ....='cd ../../../../'
alias .....='cd ../../../../'
alias .4='cd ../../../../'
alias .5='cd ../../../../..'

alias sh='bash'

alias ls='ls --time-style="+%Y-%m-%d" --color=auto'
alias la='ls -AF --time-style="+%Y-%m-%d" --color=auto'
alias ll='ls -AlF --time-style="+%Y-%m-%d" --color=auto'
alias l.='ls -alF --time-style="+%Y-%m-%d" --color=auto'

alias grep='grep --color=auto'
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'

alias bc='bc -l'

alias mkdir='mkdir -pv'

alias diff='colordiff'

alias hi='history'
alias j='jobs -l'

alias ping='ping -c 5'
alias fastping='ping -c 100 -s.2'

alias update='sudo apt-get update && sudo apt-get upgrade'

alias mv='mv -i'
alias cp='cp -i'
alias ln='ln -i'

alias today='date +%Y-%m-%d" "%H:%M:%S'
alias timestamp='date +%Y%m%d%H%M%S'

alias python='python3'

alias reboot='sudo /sbin/reboot'
alias poweroff='sudo /sbin/poweroff'
alias halt='sudo /sbin/halt'
alias shutdown='sudo /sbin/shutdown'

alias type='type -a'
alias pwd='pwd -P'

alias q='exit'
alias quit='exit'

if [ $EUID -ne 0 ]
then
    alias root='su -'
else
    alias root=''
fi

if [ $EUID -ne 0 ]
then
    alias ports='netstat -tulan'
else
    alias ports='netstat -tulanp'
fi
```
