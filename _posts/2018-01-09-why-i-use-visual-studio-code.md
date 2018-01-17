---
layout: default
title:  "[DEV] Why I choose Visual Studio Code Editor"
date:   2018-01-05 15:30:46 +0700
categories: dev
---

Tôi vẫn quen xài SublimeText để code nhưng một vài ngày này có sử dụng thử Visual Studio Code để làm việc. Thực sự nó có nhiều ưu điểm vượt trội ngoài mong đợi. Không cần config quá nhiều thứ như ST, chỉ cần thêm một vài đặc điểm là ok.

Những đặc điểm mình rất thích:
+ Có tích hợp với github
+ Khả năng diff code, review các file thay đổi, add file để commit, mọi thứ có thể làm ngay trên editor, cái này SublimeText còn thua xa, và trong số các editor gọn nhẹ mình chưa thấy có cái nào có. Với đặc điểm này có thể giúp tăng tốc độ làm việc lên nhiều lần.
+ Có đổi màu các file đã thay đổi, dễ tìm kiếm hơn
+ Giao diện đẹp, có theme Monokai
+ Có các icon đánh dấu cho file

Những điểm mình không thích:
+ Khả năng xem định nghĩa của code không hoạt động như ST

Những đặc điểm cần tự mình thêm:

```ruby
  # Tự động bỏ mấy cái khoảng trắng lúc kết thúc dòng hay vô ý thêm vào
    "files.trimTrailingWhitespace": true
  # Hiển thị dấu chấm để phân biệt khoảng trắng
    "editor.renderWhitespace": "all"
  # Set tab size is 2
    "editor.tabSize": 2
```