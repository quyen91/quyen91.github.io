---
layout: default
title:  "Generate time slot for bus booking"
date:   2020-04-15 15:30:46 +0700
categories: logic
---

# Problem
- Ví dụ tại một điểm đón xe bus A. Cần generate một list các time slot mà có xe tới đón.
Giống của trang này:
- https://www.busonlineticket.com/booking/kuala-lumpur-to-johor-bahru-bus-tickets

- Ví dụ:
+ Xe X1: 6:30AM -> 7:30PM ( 30 min một chuyến )
+ Xe X2: 7:30AM -> 8:30PM ( 15 min một chuyến )
Làm sao để ra được một list các thời điểm có xe xen kẽ nhau.

```
EX:
- 6:30:  X1
- 7:00:  X1
- 7:30:  X1
- 7:30:  X2
- 7:45:  X2
- 8:00:  X1
- 8:00:  X2
......
```

Kiểu như vậy

# Solution
-  Database chỉ lưu thời điểm start + end của các xe.
- Do đó ta cần xài một cái gì đó để generate thời gian giữa start time - end time.
- Sau khi một hồi research thì mình thấy có một kĩ thuật gọi là: CTE trong database. Đại khái nó dùng để generate sequence trong database.
- Liên kết thông tin này với time slot thì mình tìm được một hàm của postgres:
`generate_series`
- Hàm này nó có cái hay là sẽ generate ra các rows với 3 giá trị `start-end-interval`. Đây đúng là thứ mình cần vì mình cần generate tất cả các interval của thời gian cho trước. Kiểu mỗi 15min thì lại tạo một row tương ứng.

```
Ex: generate_series(6:30, 7:15, 15)
thì ta có kết quả này
- 6:30
- 6:45
- 7:00
- 7:15
```
Như vậy với mỗi range (start-end-interval) tương ứng một xe, ta đã lấy được tất cả các time slot của xe đó rồi.

Việc còn lại là ta có thể có tận 10 xe. Lúc này bằng cách join mỗi xe với generated time series của nó ta được kết quả cuối cùng.

# Key word
- Generate time slots for booking an appointment using generate series
- Generate bus schedule
- Efficient way to generate Time Slots for a schedule
- generate_series postgres
- CTE  in database