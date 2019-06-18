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

Để rõ ràng hơn nữa mời bạn hãy thử làm 1 ví dụ "Click vào button và sẽ gọi tới hàm showName". Theo lý thuyết thì sẽ tạo ra event click cho button rồi gọi tới hàm showName như một callback là xong phải không?
```javascript
const person = {
  firstName: 'Dao',
  lastName: 'Hoang',
  showName: function() {
    console.log(this.firstName + ' ' + this.lastName);
  }
}

$('button').click(person.showName); // -> undifined undifined
```
Tại sao kết quả lại ra là undifined? Vì `this` trong trường hợp này sẽ là button, nó sẽ không có firstName và lastName. Vậy thì làm sao để in ra được, ta có thể dùng bind().
```javascript
const person = {
  firstName: 'Dao',
  lastName: 'Hoang',
  showName: function() {
    console.log(this.firstName + ' ' + this.lastName);
  }
}

// `this` trong trường hợp này sẽ là person.
$('button').click(person.showName.bind(person)); // -> Dao Hoang
```


