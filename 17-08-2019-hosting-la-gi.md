# Hoisting là gì?
`Hoisting is JavaScript's default behavior of moving all declarations to the top of the current scope (to the top of the current script or the current function). - w3schools`

Hoisting là hành vi mặc định của Javascript về việc di chuyển các khai báo lên trên cùng phạm vi hiện tại ( lên đầu file script hoặc đầu current function).

Lưu ý rằng khai báo không thực sự được di chuyển. Khái niệm trên sẽ chỉ giúp các bác hiểu, bằng cách hình dung rằng các khai báo được đưa lên trên đầu phạm vi của chúng. Cùng em xem qua các ví dụ sau:

## var, let, const.
```javascript
console.log(foo); // Uncaught ReferenceError: foo is not defined
```
Chắc chắn trường hợp trên sẽ xảy ra lỗi rồi, vì mình chưa khai báo `foo`.
```javascript
console.log(foo); // undefined
var foo = 1;
```
**_What?? tại sao foo lại là undefine????_**

Okay, trong trường hợp này do mình khai báo var ngay bên dưới. `var lúc này đã được hoisted`, tức là đã được cho lên trên đầu.
```javascript
// Hình dung nó sẽ như này.
var foo;
console.log(foo);
foo = 1;
```
Đấy là `var`, thế còn `let` `const` thì sao?
```javascript
console.log(bar); // Uncaught ReferenceError: Cannot access 'bar' before initialization
let bar = 1;
```
`let` `const` sẽ không được hosted. Các bác có thể đọc thêm về [JS Let/Const](https://www.w3schools.com/js/js_let.asp).

## Function declaration và Function expression.
Trên mình đã nói về khai báo biến. Thế khai báo hàm thì có khác gì không? Trước khi đi vào phân tích thì mình sẽ cần làm rõ 2 khái niệm là `Function declaration` và `Function expression` qua ví dụ ngay dưới đây:
```javascript
// Function declaration
function foo() {

}

// Function expression
var bar = function () {

}
```

Cả 2 dạng function này, đều bị ảnh hưởng bởi hoisting.
**_Function declaration_**: toàn bộ hàm này sẽ được di chuyển lên đầu. Nghĩa là bạn có thể sử dụng nó trước khi nó được định nghĩa.
**_Function expression**: Chỉ có phần khai báo được đưa lên trên đầu

```javascript
// Function declaration
console.log(foo); // function foo
foo(); // foo
function foo() {
    console.log('foo');
}

// Function expression
console.log(bar); // undefined
bar(); // Identifier 'bar' has already been declared
var bar = function () {
    console.log('bar');
}
```
# Tổng kết.
Hoisting là hành vi mặc định của Javascript về việc di chuyển khai báo lên đầu phạm vi hiện tại.
+ `var` sẽ hosted được còn `let` và `const` thì không.
+ `Function declaration` được hosted (di chuyển cả hàm lên trên đầu phạm vi) và có thể gọi trước khi được định nghĩa. Còn `Function expression` chỉ hosted được biến (di chuyển biến lên đầu phạm vi).