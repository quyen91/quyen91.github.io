---
layout: default
title:  "Upstream is gone!"
date:   2017-09-07 15:30:46 +0700
categories: github
---

> A: branch checked out from branch `dev`
>
> B: branch checked out from branch `A`

Situtation: We finish coding in branch A and then merge A to `dev`. When we are in B, we get some notification
``` ruby
On branch source
Your branch is based on 'origin/dev', but the upstream is gone.
  (use "git branch --unset-upstream" to fixup)

```

Solution:
```ruby
git branch --unset-upstream
git branch --set-upstream-to origin/dev

```