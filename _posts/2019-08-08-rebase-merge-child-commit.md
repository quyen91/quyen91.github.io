---
layout: default
title:  "Rebase a child commit of commit merge"
date:   2019-08-08 15:30:46 +0700
categories: github
tags: git
---

We have commit tree like this:

```
1000
2000
3000
4000 - commit merge pull #abc
5000  + child 1
6000  + child 2
7000  + child 3 => need change commit name / commit author here
8000  + child 4
9000
10000
```
We can change commit name, commit author of any commit easily with `rebase`
`git rebase -i -p 7000`

But some problems happen, commit merge disappear after rebase. Now, commit tree not same as original. And there is a solution for this. We use `rebase -i -p`. Then all commit remain same as original except what we change.

Steps:

```
git rebase -i -p 7000
- vim editor open
- edit pick to edit at line 7000
- :wq -> to save

git commit --ammend
  - change author
  - change commit

```