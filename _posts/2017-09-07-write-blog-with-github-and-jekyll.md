---
layout: default
title:  "Write blog with github and jekyll"
date:   2017-09-07 15:30:46 +0700
categories: blog
---

##### To get all categories:
```ruby
categories_list = site.categories # all categories

for category in categories_list
  category[0] # name of category
  category[1].size # sum of its posts
  category[1] # list of posts
```

##### Add class to markdown content
```ruby
### Archived
{:.home-page-title}
```

##### Using dropbox for hosting image
  - Create dropbox folder share
  - Upload image
  - Copy link share
  - Change `www.dropbox.com` to  `dl.dropboxusercontent.com`

```ruby
<img class="img-responsive" src="https://www.dropbox.com/s/iqcfrs84pv1r...">
#to
<img class="img-responsive" src="https://dl.dropboxusercontent.com/s/iqcfrs84pv1r...">
```

##### View on mobile browser
- Connect computer to internet through mobile bluetooth or USB cable
- View ip for mobile connect: `ifconfig` (on linux) . IP_ADDRESS
- Edit hosts file
```ruby
# hosts file
127.0.0.1     localhost
IP_ADDRESS    localhost
```
- Binding server
```
jekyll serve --host=0.0.0.0
```