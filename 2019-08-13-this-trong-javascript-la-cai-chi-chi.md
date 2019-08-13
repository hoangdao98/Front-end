---
layout: post
title:  "[Note] This trong javascript là cái chi chi?"
date:   "2019-08-13"
categories:
---

# This trong javascript là cái chi chi?
Không có lời giải thích đơn giản nào cho `this`, nó là một trong những khái niệm làm cho kha khá "đép" phải dức đầu 😥. Hiểu sương sương **_`this` nó dùng để trỏ tới chính object gọi hàm đó_**. Vậy là xong, kết thúc bài ở đây 😬😬😬.

### Rules của this.
Để hiểu sâu hơn về `this` thì ta cần nắm chắc các rules của nó và dưới đây là những gì mình tìm được.

1. Nếu dùng từ khóa `new` để gọi function, `this` bên trong function sẽ là một object hoàn toàn mới.
```javascript
function personName() {
    console.log(this);
    this.firstName = "Dao";
    this.lastName = "Hoang";
    console.log(this);
}

new personName();

// -> {}
// -> { firstName: "Dao"; lastName: "Hoang" }
```
2. Nếu sử dụng `apply`, `call`, hoặc `bind` để gọi function, `this` bên trong function sẽ là object như đối số được truyền vào.
```javascript
function personName() {
    console.log(this);
}

var person = {
    name: "Dao Huy Hoang"
};

// this ở đây sẽ là đối số được truyền vào
var showPerson = personName.bind(person);

showPerson(); // -> { name: "Dao Huy Hoang" }
personName.call(person); // -> { name: "Dao Huy Hoang" }
personName.apply(person); // -> { name: "Dao Huy Hoang" }
//
```
3. Khi một function được gọi thông qua một object, `this` trong trường hợp này chính là object gọi đến hàm đó.
```javascript
const person = {
  lastName: 'Hoang',
  firstName: 'Dao',
  showFullName: function() {
    console.log(this.lastName + ' ' + this.firstName);
  }
}

// Ở đây this sẽ là object person
person.showFullName();
// -> "Hoang Dao";
```

4. Nếu 1 function được gọi không có rules nào ở trên thì `this` trong trường hợp này sẽ là global. Trong trình duyệt, nó sẽ là `window`. Trường hợp sử dụng strict mode ('use strict'), `this` sẽ là `undefined` thay vì là `window`.
```javascript
function person() {
    console.log(this);
}

person() // -> Window {stop: ƒ, open: ƒ, alert: ƒ, ...}

// hoặc

window.person();
```
5. Nếu áp dụng nhiều quy tắc trên, quy tắc nào lớn nhất thì `this` sẽ được áp dụng vào quy tắc đó _(1 là lớn nhất)_.

6. Nếu sử dụng ES2015 arrow function, nó sẽ bỏ qua hết tất cả các trường hợp ở trên và `this` sẽ là phạm vi xung quanh nó ở thời điểm nó được tạo ra.
```javascript
const person = {
    name: "Hoang",
    showName: () => {
        console.log(this.name);
    }
}

// This ở đây sẽ là hàm showName, trong hàm showName không có name nên kết quả sẽ là undefined.
person.showName(); // -> undefined.
```
### Thực hành.

**Trong function dưới có các quy tắc nào được áp dụng?**
```javascript
var obj = {
    value: 'hi',
    printThis: function() {
        console.log(this);
    }
};
var print = obj.printThis;
obj.printThis();
print();
```
**Khi áp dụng nhiều quy tắc trên**
> Nếu áp dụng nhiều quy tắc trên, quy tắc nào lớn nhất thì `this` sẽ được áp dụng vào quy tắc đó _(1 là lớn nhất)_.
``` javascript
var obj1 = {
    value: 'hi',
    print: function() {
        console.log(this);
    },
};
var obj2 = { value: 17 };
```
Nếu rules 2 và 3 được áp dụng, rule 2 sẽ được ưu tiên.
```javascript
obj1.print.call(obj2); // -> { value: 17 }
```
Nếu rule 1 và 3 được áp dụng, rule 1 sẽ được ưu tiên.
```javascript
new obj1.print(); // -> {}
```
# Tổng kết.
Qua cái đống hổ lốn trên 😳😳😳, em rút ra được bài học về `this` như sau:

__Giá trị của `This` sẽ phụ thuộc vào cách gọi hàm.__
1. Nếu dùng từ khóa `new` để gọi function, `this` bên trong function sẽ là một object hoàn toàn mới.
2. Nếu sử dụng `apply`, `call`, hoặc `bind` để gọi function, `this` bên trong function sẽ là object như đối số được truyền vào.
3. Khi một function được gọi thông qua một object, `this` trong trường hợp này chính là object gọi đến hàm đó.
4. Nếu 1 function được gọi không có rules nào ở trên thì `this` trong trường hợp này sẽ là global. Trong trình duyệt, nó sẽ là `window`. Trường hợp sử dụng strict mode ('use strict'), `this` sẽ là `undefined` thay vì là `window`.
5. Nếu áp dụng nhiều quy tắc trên, quy tắc nào lớn nhất thì `this` sẽ được áp dụng vào quy tắc đó _(1 là lớn nhất)_.
6. Nếu sử dụng ES2015 arrow function, nó sẽ bỏ qua hết tất cả các trường hợp ở trên và `this` sẽ là phạm vi xung quanh nó ở thời điểm nó được tạo ra.
