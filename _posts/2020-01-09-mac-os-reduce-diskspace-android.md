---
layout: default
title:  "MacOS - reduce disk space for Android Studio"
date:   2020-01-09 15:30:46 +0700
categories: os
---

### Problem
Mình đang có dự án react native dùng Android Studio để run và build, nhưng mỗi lần cài thêm cái máy ảo AVD  là mất toi mấy GB ổ cứng, Macbook thì có 128G. Nên cần phải tìm cách chạy những folder data ở một ổ cứng ngoài.

### Solution
- Ổ cứng ngoài WD
- Để an toàn nhất là copy toàn bộ folder sdk sang ổ cứng ngoài test xem chạy không đã

Có 2 folder android studio cần move tới ổ cứng ngoài

##### /android/sdk
- folder này chứa toàn bộ các tool, sdk để build app
- copy tầm 10G folder `/android/sdk` tới ổ cứng ngoài
  - Lúc mới chạy báo 3h mới xong, cứ tưởng lâu lắm, mấy lần định thử mà lâu quá nên tắt.
  - Nhưng chạy một lát khoảng 10 phút được 600M thì sau đó thì rất nhanh khoảng 15p là xong cho phần còn lại. Có lẽ 600M đầu quá nhiều file setting.
  - default: `~/Library/Android/sdk`
  - new location: `/Volumes/ABC/Android/sdk`
- Result: build ok, không lỗi gì.

##### ~/.android/avd
- Khi tải máy ảo về build thì báo lỗi do ổ cứng trên Mac của mình hết dung lượng. Thì ra do mình chưa chỉnh đường dẫn lưu `avd` nên nó vẫn trỏ tới mac.
- Việc cần làm là trỏ nơi lưu `avd` tới ổ cứng ngoài.
- Sử dụng lệnh `launchctl setenv ANDROID_AVD_HOME`
- Tham khảo từ: [https://dev.to/oscherler/move-android-studio-virtual-devices-on-a-mac-5ej5](https://dev.to/oscherler/move-android-studio-virtual-devices-on-a-mac-5ej5)
- Sau khi chạy xong, tải thử một `avd` mới về thì thấy nó đã chiếm gần 10G ổ cứng ngoài. Chứng tỏ setting đường dẫn đã working.

=> Vậy là đỡ được khá nhiều không gian lưu trữ cho Mac rồi.