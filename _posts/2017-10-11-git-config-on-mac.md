---
layout: default
title:  "[Git] Change git setting on mac"
date:   2017-09-30 15:30:46 +0700
categories: github
---

#### Reset keychain, and remove all user on mac
```ruby
git credential-osxkeychain erase
 host=github.com
 protocol=https
 <press return>
```
[Reset git credentials on MacOS](https://stackoverflow.com/questions/11067818/how-do-you-reset-the-stored-credentials-in-git-credential-osxkeychain)

#### Config for only one project
```ruby
git config user.name quyen
git config email user.email abc@gmail.com
```

#### When cannot push to github cause of switching account
```ruby
git config credential.username 'Billy Everytee'
# 'Billy Everytee` is your username in github
# Ref: https://superuser.com/a/1245296
```
