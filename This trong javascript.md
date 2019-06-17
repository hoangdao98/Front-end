Không có lời giải thích đơn giản cho `this`. Nó là một trong những thứ khó hiểu nhất trong Javascript.

## Quy tắc của `this`

1. Nếu keyword `new` được sử dụng khi gọi hàm. `This` trong function này sẽ là 1 object hoàn toàn mới.
```javascript
function exampleThis() {
  console.log(this);
  this.value = 5;
  console.log(this);
}

new exampleThis();

// -> {}
// -> {value: 5}
```

2. Nếu `apply`, `call`, hoặc `apply` được sử dụng khi gọi/tạo mới một function, `this` bên trong function là object được truyền vào là 1 đối số (argument).
```javascript
function fn() {
    console.log(this);
}
var obj = {
    value: 5
};
var boundFn = fn.bind(obj);
boundFn();     // -> { value: 5 }
fn.call(obj);  // -> { value: 5 }
fn.apply(obj); // -> { value: 5 }
```

Để rõ ràng hơn nữa mời bạn hay xem ví dụ dưới đây:

```javascript
const person = {
  firstName: 'Dao',
  lastName: 'Hoang'
  showName: function() {
    console.log(this.firstName + ' ' + this.lastName);
  }
}

person.showName(); // -> Dao Hoang
```
`this` trong trường hợp trên sẽ là object person. Cùng làm ví dụ phức tạp hơn 1 chút đó là: "Click vào button và sẽ gọi tới hàm showName", theo lý thuyết thì sẽ tạo ra event click cho button rồi gọi tới hàm showName là xong phải không?
```javascript
const person = {
  firstName: 'Dao',
  lastName: 'Hoang'
  showName: function() {
    console.log(this.firstName + ' ' + this.lastName);
  }
}

$('button').click(person.showName);
```


