---
layout: default
title: "SSH agent forwarding"
date: 2019-03-16 13:00:46 +0700
categories: devops
tags: til
---
####  No sleeping with ssh

Một ngày đẹp trời mình sử dụng ansible để deploy với ssh, connect tới server và server sẽ lấy code từ github của mình.

Nhưng mọi thứ không dễ như mình tưởng. Mình rảnh quá nên tạo cặp `key ssh private/public` ở local. Và copy public key lên server, như vậy đến đây mình ssh vào server bình thường.

Nhưng lại có vấn đề là lúc ở trên server, làm sao pull code từ github vể ? Thế là mình tạo một cặp `key ssh private/public` trên server. Sau đó thêm public key vào github thì lúc này trên server có thể dùng command pull code github về.

Nhưng khi deploy auto bằng capistrano thì `ssh-agent` một chương trình chạy nền lưu ssh key trong memory không thể start agent pid của cặp key trên server. Nên chỉ ssh được vào server mà không thể pull code từ github vể server.

Tìm hiểu ra thì mới biết có một thứ gọi là `SSH agent forwarding`, một thứ mà mình có xài nhưng không hiểu gì về nó. Đại khái như trường hợp của mình chỉ cần một cặp key private/public ở local, server cũng dùng key đó cho các service khác dùng ssh connection, thay vì phải generate một cặp key nữa trên server.

Seting `SSH agent forwarding` như thế nào?
- sửa file ~/.ssh/config
- Thêm vào đoạn config sau:

``` bash
Host myhost.com # or: IP
  ForwardAgent yes
```

hoặc `ssh -A user@myhost.com `
- `-A` là flag sử dụng thay cho config ở trên

Để test thì ta ssh vô server sau đó pull repo private nào đó thử. Hoặc chạy lệnh `ssh -T git@github.com` xem có authen đúng user github không.

---
References:

  - [dev.to - ssh agent forwarding](https://dev.to/levivm/how-to-use-ssh-and-ssh-agent-forwarding-more-secure-ssh-2c32)