---
layout: default
title:  "Load more when truncate text react native"
date:   2019-09-05 15:30:46 +0700
categories: react-native
---

Problem:
- Cần truncate một đoạn text, limit là 2 dòng trong react native
- Cần có một icon load more khi mà text được truncate, ẩn đi nếu đã hiển thị fulltext

Solution:
- React native có một thuộc tính là `numberOfLines` và khi ta set thuộc tính này thì có thể tạo được một đoạn text được truncate 2 lines.

``` js
<View style={styles.container}>
  <Text numberOfLines={2} style={styles.text}> This is a very long text </Text>
</View>

var styles = StyleSheet.create({
  container: {
    flexDirection: 'row',
    padding: 10
  },

  text: {
    flex: 1
  }
});
```

Nhưng có một vấn đề là khi áp dụng cho tiếng Nhật, tiếng Việt hay ngôn ngữ có chứa một số kí tự đặc biệt thì việc tạo text truncate không còn chính xác nữa.  Thực tế mình thấy có lúc chỉ hiện thị một dòng, có lúc thì truncate không được.
Thứ hai là vì mình cần một icon load more ẩn hiện dựa trên việc text được truncate hay không. Vậy làm sao biết được ?

Nên mình không dùng `numberOfLines` nữa. Mà dựa vào chiều cao của text để làm. Khi truncate thì chiều cao của text là 2 dòng, khi fulltext thì không set chiều cao.

Để làm được thì thẻ `<Text></Text>` phải set `lineHeight` cố định để biết height của một dòng. Từ đó kết hợp với `onLayout`của `<View></View>` bao ngoài để tính chiều cao của đoạn text khi hiển thị full.

```js
<View onLayout="handleHeight">
  <Text height="textHeight"> long text </Text>
</View>

function handleHeight(){
  // Ex:
  lineHeight = 10
  if totalViewHeight > lineHeight
    textHeight = 22
  else
    textHeight = undefined

  // Set các status cho việc truncate
  // Ở đây ta có thể set state status để ẩn hiện button loadmore
}
```

