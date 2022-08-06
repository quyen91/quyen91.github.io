---
layout: default
title:  "Make sure that `gem install puma -v '2.10.2' --source 'https://rubygems.org/'` succeeds before            
bundling"
date:   2022-08-06 01:30:46 +0700
categories: rails
tags: os
---

### Problem: 
I have old version puma with ruby 2.2.2. It throws this error when bundling.
```
An error occurred while installing puma (2.10.2), and Bundler cannot continue.
Make sure that `gem install puma -v '2.10.2' --source 'https://rubygems.org/'` succeeds before            
bundling. 
```
I know that my current openssl version on my Ubuntu 20.4 is 1.1.0. And puma are requiring openssl 1.0. 
I also tried to install both versions of openssl. But it made mess of package.
You can check here for ref installing custom version . [Install openssl 1.0](https://www.howtoforge.com/tutorial/how-to-install-openssl-from-source-on-linux/)

After installing ruby 2.2.2. I see there is one openssl@1.0.2 in `~/.rbenv/versions/2.2.2/openssl/`. But system ignoring this version when bundling with error: 

```
In file included from /usr/include/openssl/e_os2.h:13,
                 from /usr/include/openssl/bio.h:13,
                 from mini_ssl.c:4:
/usr/include/openssl/ssl.h:1895:1: note: declared here
 1895 | DEPRECATEDIN_1_1_0(__owur const SSL_METHOD *DTLSv1_method(void)) /* DTLSv1.0 */
      | ^~~~~~~~~~~~~~~~~~
mini_ssl.c: In function ‘engine_read’:
mini_ssl.c:164:14: warning: unused variable ‘n’ [-Wunused-variable]
  164 |   int bytes, n;
      |              ^
mini_ssl.c: In function ‘engine_write’:
mini_ssl.c:187:8: warning: unused variable ‘buf’ [-Wunused-variable]
  187 |   char buf[512];
      |        ^~~
make: *** [Makefile:238: mini_ssl.o] Error 1

make failed, exit code 2

```

# Solution
First, I tried with this command. System still ignore openssl folder
```
gem install puma -v '2.10.2' --source 'https://rubygems.org/' -- --with-openssl-dir=~/.rbenv/versions/2.2.2/openssl
```


Second, I tried with this

```
gem install puma -v '2.10.2' --source 'https://rubygems.org/' -- --with-cppflags=-I/home/kupro20/.rbenv/versions/2.2.2/openssl/include
```

And OMG, it is working. I can install gem and bundle successfully.


---- 
Reference: 
[Error install gem with openssl verison](https://stackoverflow.com/a/30836309/3551956)
