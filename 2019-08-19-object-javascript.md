# Khái niệm về object?

Một đối tượng (object) là một danh sách các item, mỗi item là một cặp name-value, trong đó value có thể là: các dữ liệu cơ bản (Number, String, Boolean, Undefined, Null), function, hoặc có thể là một object khác.

Nếu item trong object là một function thì ta gọi nó là method (phương thức của một object), còn không thì nó sẽ là property (thuộc tính).

```javascript
var obj = {
  name: "value",
  number: 10,
  isKimochi: true,
  girlFriend: undefined,
  money: null,
  learning: function() {
    return "reactjs";
  },
  jobs: {
    name: "Frontend"
  }
};
```

Ta có thể thấy obj trên đang có 1 list các item, và nó đi theo cặp name-value được cách nhau bởi ký tự `:`.

# Khởi tạo object.

Ta có 3 cách để tạo ra 1 object đó là `object literal`, `object constructor` và `Object.create()`.

### Object literals

Object literals sẽ dùng dấu `{}` để tạo ra một object.

```javascript
var me = { caigiday: "20cm" }; // Khoi tao object literals

console.log(me);
```

### Object constructor

Cách này sẽ sử dụng phương thức khởi tạo (constructor) của kiểu dữ liệu object để tạo ra object.

```javascript
// Dùng new Object() để tạo đối tượng mới.
var foo = new Object(); //

console.log(foo);
```

### Object.create()

Cách này sẽ tạo một object mới sử dụng một object hiện có, để cung cấp prototype cho object mới sẽ được tạo ra.

**_Cú pháp:_** `Object.create(prototypeObject, propertiesObject)`

- prototypeObject: Object prototype mới được tạo ra. Có thể là null hoặc object.
- propertiesObject (optional): Các thuộc tính của object mới.

```javascript
var me = Object.create(null);
console.log(me); // {}
```

**Ví dụ**

Mặc định ta phải có prototypeObject (có thể là object hoặc là null). Nó là bắt buộc, không được để trống.

```javascript
var you = {
  firstName: "Mini",
  lastName: "Diva",
  showName: function() {
    console.log(this.firstName + " " + this.lastName);
  }
};

// Khởi tạo object `me` với prototype của you.
var me = Object.create(you);

me.firstName; // Mini
me.lastName; // Diva
```

Ta tiếp tục tìm hiểu propertiesObject (optional) để xem cách hoạt động của nó như nào. Theo lý thuyết propertiesObject là:

> Optional. If specified and not undefined, an object whose enumerable own properties (that is, those properties defined upon itself and not enumerable properties along its prototype chain) specify property descriptors to be added to the newly-created object, with the corresponding property names. These properties correspond to the second argument of Object.defineProperties().

Hiểu nôm na rằng các thuộc tính này tương ứng với đối số thứ 2 của [Object.defineProperties()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperties) (props) nếu propertiesObject được định nghĩa. Còn không thì sẽ không có gì cả (undefined).

**Có tàm tạm lí thuyết rồi vậy thực hành thôi**

```javascript
// Cách sử dụng propertiesObject
var person = Object.create(
  {},
  {
    me: {
      value: 'male' // Cần phải dùng value để gán giá trị
    },
    you: 'female' // Nếu không dùng thì sẽ bị lỗi
    // Uncaught TypeError: Property description must be an object
  }
);
```
Ngoài value ra thì nó sẽ có một sô thuộc tính khác như là `configurable`, `enumerable`, `value`, `writable`, `get`, `set`.

# Chưa hoàn thành ...