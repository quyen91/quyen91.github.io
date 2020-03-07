---
layout: default
title:  "Change git setting on mac"
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

#### Using many account github on mac
```ruby
# https://gist.github.com/hkasera/bcdac17ff11d6442130a

eval "$(ssh-agent -s)"
ssh-add -K ~/.ssh/id_rsa

ssh-add ~/.ssh/quyen91_github
```

#### When pull from other account/organization
```ruby
# https://tiffanybbrown.com/2017/06/using-multiple-ssh-keys-with-github/index.html

 Edit file .git/config

  url = git@github.com-second_user_name:org-name-if-applicable/reponame.git
  ex:
  url = git@github.com-quyen91:airbn/reponame.git
```