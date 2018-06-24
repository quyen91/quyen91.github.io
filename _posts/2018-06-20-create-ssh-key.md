---
layout: default
title:  "Create ssh key"
date:   2018-01-27 15:30:46 +0700
categories: devops
---

```ruby
# Create new file key
ssh-keygen -t rsa -b 4096 -C "my@email.com" -f ~/.ssh/new-key-file
# => this create private(new-key-file) + public key(new-key-file.pub)

nano ~/.ssh/config

Host my-server
  HostName 112.3.87.11
  User deploy
  Port 22
  TCPKeepAlive yes
  IdentityFile

# Login server
ssh my-server

# Set public key on server
# create file `~/.ssh/authorized_keys`
# Add new line is content of file: new-key-file.pub

# In capisino
set :ssh_options, {
  forward_agent: true,
  auth_methods: ["publickey"],
  keys: ["~/.ssh/my-project"]
}

# remove all keygen and ssh mac

# https://askubuntu.com/questions/929934/how-to-create-multiple-ssh-keys?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa
# https://kb.iu.edu/d/aews#id

```