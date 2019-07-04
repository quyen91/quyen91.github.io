---
layout: default
title:  "Round with js"
date:  2019-07-04 15:30:46 +0700
categories: js
---

Tình huống:

Khi sử dụng thư viện [star-rating-svg](https://github.com/nashio/star-rating-svg) thì gặp phải chuyện tỉ lệ rating star. Ví dụ 2.3 -> thì làm tròn lên 2.5, 2.1 làm tròn xuống 2, 2.6 thì làm tròn xuống 2.5. Nhưng thư viện này nó mặc định làm tròn gần nhất tới 1, 2, 3..... Cái mình mong muốn là làm tròn theo kiểu: 1, 1.5, 2, 2.5.... Vậy nên phải xài hàm `Math.round` của js

```javascript
val = Math.round(val * 4) / 4; /* To round to nearest quarter */
val = Math.round(val * 2) / 2; /* To round to nearest half */
```

tương tự ta có thể suy ra
```javascript
val = Math.round(val * 8) / 8;
```
nếu muốn làm tròn tới mức nhỏ hơn.

------
References:

[Jquery Star Rating Plugin - Half star Not Working](https://stackoverflow.com/questions/1987524/turn-a-number-into-star-rating-display-using-jquery-and-css?fbclid=IwAR0kzLWJEYe6NntR1-YhlIhaHlO_-1hrCoAU7_m2MRzLod5kWQKjP3kO_yc)