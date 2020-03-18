---
layout: default
title: "Unable to install manjaro - the installer failed to create partition on disk"
date: 2020-03-12 15:30:46 +0700
categories: os
---

# Problem
- Lúc mới cài tưởng dễ ăn , ai dè đến bước tạo partition thì ăn hành, bị lỗi `Unable to install manjaro - the installer failed to create partition on disk`. Dùng `KDE -Partition Manager` thì cứ bắt nhập pass mà rõ ràng mình đang boot bằng usb. Lấy đâu ra pass.

# Solution
- Do chả hiểu nó set cái gì trong file cài mà cứ mở cái gì lên cũng đòi pass. Nên mình nghĩ do có password nên nó ko tạo được partition.
- Mình tải về GParted. Dùng `sudo gparted` mới mở được
- Sau đó tạo các phần vùng (`swap` - 5G, `/home` - 20G, `/` - 20G, `/boot` - 500Mb). Đại khái là cho nó tạo và format partition trước. Vì lúc nãy mở Gparted bằng `sudo` nên nó format và tạo partition ok hết.

- Và thế là kết thúc tốt đẹp. Mọi thứ cài ok .

#  Lỗi của định mệnh: file ‘/boot/grub/i386-pc/normal.mod’ not found

- Dùng lệnh này để tìm ra tất cả các ổ đĩa có file system ext2 `ls (hd0,msdos1)`
- Sẽ có 3 ổ như lúc mình tạo phần vùng
- Dùng `ls (hd0,msdos1)/` để xem cái nào là root
- Khổ nỗi tất cả các disk đều không có thư mục đó.

=>  Bó tay tập 1.

# Con đường gian nan: cài lại Xubuntu.
- dùng rufus: lúc tạo usb cài chọn GPT - chứ ko phải MBR
- Lần này nhanh gọn không cần tạo nhiều phần vùng: tạo 1 swap + 1 root
- Cuối cùng vào boot vẫn không được bị văng ra grub rescue `file ‘/boot/grub/i386-pc/normal.mod’`
- Thử đủ mọi cách vẫn không được

=> Bó tay tập 2.

# Cuối cùng cũng tới đích
- Tìm thấy tuts này: [Using boot repair từ usb cài](https://www.maketecheasier.com/recover-from-the-file-not-found-grub-rescue-screen/)
- Mình làm theo hướng dẫn, cài grub lên phân vùng `root`.
- Restart thì ôi đã vào được linux.
- Nhưng mất tiêu cái menu chọn window, linux.
- Nhưng nhớ ra là phải dùng lệnh huyền thoại cài lại grub trên cái /dev/sda

  `sudo update-grub`

  `sudo grub-install /dev/sda`

- Thế là xong. Vào được menu boot