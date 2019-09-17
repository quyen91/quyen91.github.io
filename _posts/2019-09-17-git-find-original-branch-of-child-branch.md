---
layout: default
title:  "Git - find parent branch of child branch"
date:   2019-09-17 15:30:46 +0700
categories: github
---

### Problem:
```
A_branch:
  - commit a1
  - commit a2
  - ......

A_branch - checkout -> B_branch

B_branch:
  - commit a1
  - commit a2
  - ......
  - commit b1
  - commit b2
  - ......
```

A few time later, when we on branch B, but we forget what branch we checkout from. How do we know that A is parent of B ?

### Solution:
Using `reflog` and `grep`, we can do it.
When we on branch A_branch and run `git checkout -b B_branch`, we will see some logs with `reflog`:

```bash
.....
......
85b4b25 HEAD@{150}: checkout: moving from A_branch to B_branch
85b4b25 HEAD@{150}: checkout: moving from B_branch to XYZ
85b4b25 HEAD@{152}: checkout: moving from A_branch to B_branch
```

So we need keyword: `to B_branch`, in last line (last activity log)

```
git reflog | grep "to $(git rev-parse --abbrev-ref HEAD)" | tail -1

// return
// 85b4b25 HEAD@{152}: checkout: moving from A_branch to B_branch
```

So, A_branch is parent of B_branch