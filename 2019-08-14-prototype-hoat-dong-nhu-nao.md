---
layout: post
title:  "[Note] Bạn đã thực sự hiểu về Prototype?"
date:   "2019-08-13"
---

# Prototype hoạt động như nào?
Đây là câu hỏi phỏng vấn javascript cực kỳ phổ biến. Tất cả object trong javascript đều có 1 prototype ( nôm na nó là khuôn mẫu hoặc là cha của một object ), nó còn là một tham chiếu đến 1 object khác. Khi một thuộc tính được gọi bởi 1 object và nếu không tìm thấy trong object đó thì javascript engine sẽ tìm đến object's prototype. Tìm đến khi nào nó thấy property hoặc khi đến prototype cuối cùng. Nó có phần giống class, được sử dụng cho việc kế thừa (interitance) trong javascript.

## Ví dụ

``` javascript
var parent = function() {
 this.name = "Dao Huy Hoang";
}

parent.prototype.greet = function() {
    console.log("Hello Dao Huy Hoang");
}

const child = Object.create(parent.prototype);

child.smile = function() {
    console.log("ư ư ư ư!");
}

child.smile(); // -> ư ư ư ư!

child.greet(); // -> Hello Dao Huy Hoang
```

Những điều cần lưu ý:
* .greet() không được định nghĩa ở child. Vì vậy javascript engine sẽ tìm .greet bên trong prototype được kế thừa từ parent.

* Chúng ta cần gọi Object.create() theo một trong những cách sau cho việc kế thừa prototype.
    + `Object.create(Parent.prototype);`
    + `Object.create(new Parent(null));`
    + `Object.create(objLiteral);`
    + Hiện tại, `child.prototype` đang được trỏ đến `parent`:

```javascript
child.constructor;
ƒ () {
    this.name = "Parent";
}
child.constructor.name
"Parent"
```

Nếu muốn sửa lỗi này, chúng ta có thể làm như sau:
```javascript
var parent = function() {
 this.name = "Dao Huy Hoang";
}

parent.prototype.greet = function() {
    console.log("Hello Dao Huy Hoang");
}

function Child() {
  parent.call(this);
  this.name = 'child';
}


Child.prototype = parent.prototype;
Child.prototype.smile = function() {
    console.log('ư ư ư ư!');
}
Child.prototype.constructor = Child;

var c = new Child();

c.smile(); // -> ư ư ư ư!

c.greet(); // -> Hello Dao Huy Hoang

c.constructor.name; // -> "Child"
```

# Tổng kết.
Từ những thứ em mới viết bên trên thì em sẽ rút ra được bài học về prototype như sau:
* Prototype sẽ tham chiếu đến 1 object khác, và khi property được gọi bởi một object, nếu không tìm thấy trong object đó thì javascript engine sẽ tìm đến object's prototype, đến khi nào tìm thấy property hoặc prototype cuối cùng.
* Do Javascript không có khái niệm class, do vậy, prototype sẽ dùng để kế thừa các trường/hàm của 1 object.

### Nguồn tham khảo.


