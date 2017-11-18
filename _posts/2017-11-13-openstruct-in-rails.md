---
layout: default
title:  "[RAILS] Openstruct in rails "
date:   2017-11-13 15:30:46 +0700
categories: rails
tags: openstruct
---

Preparation:
 - OpenStruct là gì?
 - Cấu trúc như thế nào?
 - Khi nào dùng?
 - Dùng như thế nào

```ruby
my_struct = OpenStruct.new name: "Quyen", age: 20
my_struct.name  # => Quyen
my_struct.age # => 20
```

Usage:
- Ta có thể đọc dât từ file .yml vào một mảng OpenStruct (ví dụ setting cho plan user, member level...)
`[vn: <OpenStruct>, en: <OpenStruct>, ....`]

[Tìm hiểu thêm openstruct](https://viblo.asia/p/cau-truc-du-lieu-openstruct-LzD5dABoKjY)