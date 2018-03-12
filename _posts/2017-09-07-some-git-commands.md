---
layout: default
title:  "[Git] Some git commands"
date:   2017-09-07 15:30:46 +0700
categories: github
---

``` ruby
#### Thay đổi tên commit cuối cùng
git commit --amend

#### Kết hợp nhiều commit thành một
git rebase -i HEAD~5

#### Xem lịch sử các commit, merge...
git reflog

#### Undo a commit
git reset 'HEAD@{1}'

#### Undo commit but keep file changed
git reset --soft HEAD~1 #or
git reset --soft 2ed26e52092851f40ea4fec60d357cd138f04209

#### Hủy bỏ các commit đã thực hiện trước đó, cả những commit merge...
git reset --hard HEAD@{N}

#### Combine nhiều commit thành một với git flow finish
git flow feature finish -S branch_name

#### Reset file
git reset HEAD filename
git checkout -- filename
git reset --hard origin/master # Reset all file and return to origin/master

#### CHeckout a file to a branch
git checkout origin/master filename

#### Run code on special commit
git checkout 2ed26e52092851f40ea4fec60d357cd138f04209
git checkout current_branch # To exit detach mode

# https://stackoverflow.com/a/1817774/3551956

#### Rename author github commit
git rebase -i <earliercommit>
git commit --amend --author="Author_Name <email@address.com>"

+ Change pick -> edit
+ rebase continue

# https://stackoverflow.com/a/3042512/3551956
# https://gist.github.com/trey/9588090
```

- [Git flow cheat_sheet](https://github.com/nvie/gitflow/wiki/Command-Line-Arguments)
