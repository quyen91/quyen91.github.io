---
layout: default
title:  "Thay đổi size của partition ext4 linux - lubuntu"
date:   2017-09-30 15:30:46 +0700
categories: OS
tag: linux, lubuntu
---

- Vấn đề:

  Đang sử dụng lubuntu(song song với window) - mình thích OS  này vì nó phù hợp với phong cách của mình hơn ubuntu hay những OS khác. Lúc mới cài đặt thì dùng `23Gb - root, 8Gb - home, 5Gb - swap`.
   Ai biết được sau khi cài đặt ruby, gem, module npm... thì dung lượng của `/home` ngày càng tăng lên, cuối cùng gần đây còn lại có `800Mb`. Thế là quyết định tăng dung lượng nó lên bằng các free partition còn lại.

Nếu cài lại OS từ đầu thì đơn giản nhưng phải cài lại các tool dev các nhau...và còn nhiều thứ liên quan tới mấy cái projects, config rất mất thời gian.

- Giải pháp

  Tạo một free partition - 10G từ một ổ NFST trong window sau đó extend `/home` với partition đó.

### #1: Tạo ra free partition trong window
- Dùng [MiniTool Partition Wizard](https://www.partitionwizard.com/) tạo một partition trống 10G từ một ổ đĩa C/D/E gì đó. Tốt nhất tạo ra nó ngay sau partition ext4 muốn extend. Tool này làm khá đơn giản, dữ liệu an toàn không vấn đề gì cả và cũng nhanh nữa.


    ![quyencarrot - mimitool partion](https://dl.dropboxusercontent.com/s/l5l2bnr6e31qb8h/window1.jpg?dl=0)

- Lỗi boot sau khi reboot

   Sau khi cài xong reboot lại thì gặp lỗi màn hình đen thui: `Error: unknow filesystem`

   ![quyencarrot - error filesystem unknown](https://dl.dropboxusercontent.com/s/j6lvr1901hqs3d1/boot2.jpg?dl=0)


   Tuy nhiên sau khi google thì đã có cách
  ```ruby
    # Dùng cmd: ls để show các partition
    ls
    set prefix=(hd0,msdos1)/boot/grub # Cái này phải mò nếu set đúng partition mới chạy, có thể thử nhiều lần
    insmod normal
    normal

    # Sau khi thành công vào linux thì update lại grub
    sudo update-grub
    sudo grub-install /dev/sda
 ```
 Ref: [Quora - fix error unknown filesystem](https://www.quora.com/How-do-I-fix-a-grub-rescue-unknown-file-system-error/answer/Amit-Kumar-Padal?srid=2eVF)
- Kết quả tạo được free partition mới `10G`, fix được boot

  Nhưng đời méo có như mơ, không resize được ext4 partition bằng MiniTool Partition. Đành qua linux để xử lí. Bên này có vài cách để extend ext4 partition:
   + Dùng `Gparted` (OS của mình lâu không update, lỗi nên méo cài được)
   + Dùng bootable usb (Đơn giản là không thích dùng, cảm giác không an toàn)
   + Dùng cmd với các tool tích hợp sẵn tron OS (cool)

### #2: Extend partition ext4 được mount tới `/home`
  Sau khi đọc tài liệu thì thấy có giải pháp đơn giản là dùng `resize2fs /dev/sd6 10G` (ví dụ hiện tại `/dev/sd6` đang là 5G) nhưng điều này là không thể. Partition size là 5G thì filesystem chỉ extend tới tối đa 5G. Nếu dùng `resize2fs /dev/sd6 2G` thì ok. Partition định nghĩa bằng `start sector - end sector` nó sẽ chứa filesystem - chứa data.

  Như vậy phải qua 2 bước
   1. Extend the partition (`fdisk`)
   2. Extend the filesystem (`resize2fs`)

  Hiện tại mình muốn extend `dev/sda8` với khoảng freespace ngay sau nó là `12.1G`

  ![quyencarrot - extend partion ext4](https://dl.dropboxusercontent.com/s/2lo63v7xuhew9e4/freespace.png?dl=0)

  Nếu dữ liệu rất quan trọng thì hãy backup vì không ai biết trước những lỗi bất ngờ.


##### 1. Sử dụng `fdisk`
  - Xóa `/dev/sda8` (cái này sẽ không xóa data, nó chỉ định nghĩa lại partition với `[start sector - end sector] + size` nên k phải lo)

  ```python
  fdisk /dev/sda
  print the partitions (p)
  delete the partition /dev/sda8 (d) # chú ý start-sector của partition này vì khi tạo partition mới cũng phải bắt đầu ở start-sector đó nếu không dữ liệu sẽ mất.
  save and exit (wq)
  ```
  - Tạo partition mới

  ```python
  fdisk /dev/sda
  print the partitions (p)
  create the partition (n)
  select the partition type (l)
  assign the number to partition (9) # Should be default
  first sector () # hãy nhớ lại cái start-sector của /dev/sda8 vừa mới xóa, nếu giống với default thì ok, không thì phải nhập lại - be carefull
  last sector () # Hãy nhập +nG  n:sizecủa partition mới, G:đơn vị Gb
  save and quit (wq)
  # Như vậy hệ thống tự động tìm các freespace để extend đủ size ta muốn. Cân nhắc giữa freespace và size partition mới cho phù hợp
  # Reboot để áp dụng thay đổi
  ```

  ![quyencarrot - fdisk resize partion - linux](https://dl.dropboxusercontent.com/s/ibjfi63ejkln1mz/fdisk.png?dl=0)


##### 2. Sử dụng `resize2fs`
Sau khi thay đổi partition có tác dụng ta mới extend filesystem. Chỉ đơn giản chạy lệnh `resize2fs /dev/sd9` để filesystem tự động extend tới max size của partition

Kết quả là đã extend được `/home` của mình thêm `10G` nữa mà không bị ảnh hưởng gì đến data hay các tool khác. Giờ thì vi vu lướt web và làm việc thôi.

![quyen - resize ext4 partition](https://dl.dropboxusercontent.com/s/ujgk9vzl1vvxt18/result.png?dl=0)


***

##### References:

  - [Youtube - Linux with fdisk](https://www.youtube.com/watch?v=_Mp3Y4RWkjA)
  - [http://positon.org/resize-an-ext3-ext4-partition](http://positon.org/resize-an-ext3-ext4-partition)
  - [http://linuxsay.com/t/how-to-resize-the-partition-in-ext4-filesystem/1489/12](http://linuxsay.com/t/how-to-resize-the-partition-in-ext4-filesystem/1489/12)