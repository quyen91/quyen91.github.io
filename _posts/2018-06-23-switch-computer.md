---
layout: default
title:  "SWITCH COMPUTER!"
date:   2018-06-23 15:30:46 +0700
categories: devops
---

Mỗi lần đổi máy, cài lại win, hay update gì đó mà liên quan tới việc xoá hết data là thấy nản. Vì nhiều cái config không muốn phải mò mẫm config từ đầu.

Đối với mac mỗi lần chuyển máy thường làm thế này:
- Copy tất cả thư mục project với git đang làm giở, vì ko phải cái nào cũng push lên git rồi
- Backup một số database quan trọng để import trên máy mới
- Copy github config file đỡ phải cài từ đầu
- Copy thư mục ~/.ssh vì nó chứa tất cả key cho việc deploy, ssh server ....
- Copy editor config setting file: VS hay SublimeText
- Export and copy bookmark browsers

Cài lại cả đống thứ cần thiết:
- Editor, Postman, Iterm(config for iterm)
- Node, Java, Ruby, RVM, Elasticsearch, Redis, Database(postgresql, mysql2)

Một số config liên quan đến ternimal: auto tab file, folder, git branch, color path....

```bash
parse_git_branch() {
  git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="\u@\h \[\033[32m\]\w\[\033[33m\]\$(parse_git_branch)\[\033[00m\] $ "

export CLICOLOR=1
export LSCOLORS=GxFxCxDxBxegedabagaced

git_branch () { git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/\1/'; }
HOST='\033[02;36m\]\h'; HOST=' '$HOST
TIME='\033[01;31m\]\t \033[01;32m\]'
LOCATION=' \033[01;34m\]`pwd | sed "s#\(/[^/]\{1,\}/[^/]\{1,\}/[^/]\{1,\}/\).*\(/[^/]\{1,\}/[^/]\{1,\}\)/\{0,1\}#\1_\2#g"`'
BRANCH=' \033[00;33m\]$(git_branch)\[\033[00m\]\n\$ '
PS1=$USER$HOST$LOCATION$BRANCH
PS2='\[\033[01;36m\]>'


if [ -f ~/.git-completion.bash ]; then
  . ~/.git-completion.bash
fi
```