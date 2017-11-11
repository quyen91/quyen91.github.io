---
layout: default
title:  "Some git commands"
date:   2017-09-07 15:30:46 +0700
categories: github
---


#### Thay đổi tên commit cuối cùng
`git commit --amend`

#### Kết hợp nhiều commit thành một
`git rebase -i HEAD~5`

#### Xem lịch sử các commit, merge...
`git reflog`

#### Hủy bỏ các commit đã thực hiện trước đó, cả những commit merge...
`git reset --hard HEAD@{N}`

#### Combine nhiều commit thành một với git flow finish
`git flow feature finish -S branch_name`

- [Git flow cheat_sheet](https://github.com/nvie/gitflow/wiki/Command-Line-Arguments)
