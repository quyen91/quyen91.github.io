---
layout: default
title:  "Can't boot into window after deleting ubuntu partition"
date:   2020-10-18 01:30:46 +0700
categories: linux
---

## Problem
- I have window and ubuntu dual-boot. When I am in window, I delete ubuntu partition by disk management. Then I can't boot into window, my laptop only show grub menu.

## Solution
 Using `efibootmgr` by below steps:

+ Using USB boot of Ubuntu.
+ Select trying linux ( without install)
+ Open ternimal
+ `sudo efibootmgr` ( show all boot )
+ `sudo efibootmgr -b 1 -B` ( delete ubuntu entry in menu boot order )
=> It's working now. I can boot into window.

-----------------
 References:
- https://askubuntu.com/a/923231