---
layout: default
title:  "Rebase a child commit of commit merge"
date:   2019-08-08 15:30:46 +0700
categories: github
tags: git
---

We have commit tree like this:

```
1000 - commit 1
2000 - commit 2
3000 - commit 3
4000 - commit merge pull #abc
5000  + commit child 1
6000  + commit child 2
7000  + commit child 3 => need change commit name / commit author here
8000  + commit child 4
9000 - commit 9
10000 - commit 10
```
We can change commit name, commit author of any commit easily with
`git rebase -i`

But some problems happen, commit merge disappear after rebase. Now, commit tree not same as original. Like this:

```
1000 - commit 1
2000 - commit 2
3000 - commit 3
5000  + commit child 1
6000  + commit child 2
7000  + commit child 3 after edit
8000  + commit child 4
9000 - commit 9
10000 - commit 10
```

And there is a solution for this. We use `git rebase -i -p`. Then all commit remain same as original except what we change.

Steps:

```
git rebase -i -p 7000
- vim editor open
- edit pick to edit at line 7000
- :wq -> to save

git commit --ammend
  - change author
  - change commit
  - :wq -> to save

```
And result:

```
1000 - commit 1
2000 - commit 2
3000 - commit 3
4000 - commit merge pull #abc
5000  + commit child 1
6000  + commit child 2
7000  + commit child 3 after edit
8000  + commit child 4
9000 - commit 9
10000 - commit 10
```