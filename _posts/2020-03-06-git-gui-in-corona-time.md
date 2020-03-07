---
layout: default
title: "Git GUI in Corona time"
date: 2020-03-06 15:30:46 +0700
categories: git
---

# Problem
Bạn rất giỏi Git CLI nhưng đến một lúc nào đó công việc ngập mặt, bạn không còn thời gian ngồi gõ lệnh, hay ngồi xem file change bằng `git diff`. Bạn cũng không thể có cái nhìn bao quát, nhanh mình đã đổi bao nhiêu file, đổi những gì. Do vậy nhiều khi gấp gáp bạn commit nhầm, commit thừa. Làm sao để giải quyết đây?

Những chức năng mà Git GUI nên có:
- Khả năng xem tổng quan mình change code những file nào, đổi gì ?
- Phần diff code nên giống github là tốt nhất
- Đơn giản dễ nhìn
- Luôn update async với file change trong máy
- Khả năng merge, merge squash, stash...nhanh.

# Solution

Chắc chán là Git GUI roài, nhưng hiện tại có những tool nào xài ngon?
Bản thân mình từng xài nên sẽ đánh giá 2 thằng cho 2 nền tảng.

#### Fork - the best on Mac OS
  Theo mình cảm nhận thì đây là thằng hay nhất mình từng xài

  `Ưu điểm:`

   - Nhẹ, nhanh (nhất là so với Gikraken)
   - Giao diện để sử dụng, đẹp nữa
   - Chỉ có những chức năng cần thiết nên không bị rối khi nhìn
   - Các thao tác như merge, stash, reset, commit rất dễ xài và nhanh
   - Cái hay nhất là phần diff file của nó, rất trực quan, diff giống như trên github vậy. Còn dễ nhìn hơn vscode.
   - Rất ít khi mình thấy nó bị lỗi kiểu như file change mà không reload
   - Free

 ` Nhược điểm`

   - Chỉ xài được trên Mac/Win, trên Linux sao lại không có cơ chứ?
   - Sau này có thể bắt trả phí, nhưng nếu cần mình sẽ sẵn sàng trả phí để xài.

#### Sublime Merge  - the best on Linux
  Đến thời điểm hiện tại mình đã thử qua khá nhiều Git GUI trên linux mà không có cái nào hài lòng cả. Chỉ có cái Sublime Merge này thì có vể hợp với ý mình nhất.

  `Ưu điểm`

  - Xài được trên Linux
  - Chức năng diff file khá ổn, giống github nhưng kém Fork một chút nhưng cũng tạm chấp nhận được
  - Thấy khá nhanh và nhẹ
  - Chỉ có những chức năng cần thiết, không bị rối mắt
  - Free

  `Nhược điểm`

  - Phần diff code, xem file change mình vẫn chưa ưng lắm, nhìn vẫn khá là rối.
  - Hiệu năng mình sẽ thử xài một thời gian lâu lâu xem sao, rồi review tiếp