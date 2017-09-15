---
layout: default
title:  "[BlOG] Some important variables in Jekyll"
date:   2017-09-07 15:30:46 +0700
categories: blog_config
---

To get all categories:
```ruby
categories_list = site.categories # all categories

for category in categories_list
  category[0] # name of category
  category[1].size # sum of its posts
  category[1] # list of posts
```