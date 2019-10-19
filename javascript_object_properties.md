#### Object Properties
  > Properties are the most important part of any JavaScript object.
 - Properties là những giá trị được gán cho 1 đối tượng trong JS
 - Một Object JS là một tập hợp các properties không sắp xếp
 - Properties có thể thường xuyên được thay đổi, thêm mới, và deleted, nhưng cũng có trường hợp readonly
 #### 1. Truy cập một Javascript Properties
   - Có 3 cách truy cập vào một properties
      * objectName.property, ví dụ : ```person.age```
      * objectName['property'], ví dụ: ```person["age"]```
      * objectName[expression], ví dụ: ```x = "age"; person[x]```
   - Access to all properties of object
  ```javascript
    var person = { fName:"Thieu", lName:"Le", age:18 };
    
    for (x in person) {
      txt += person[x];
    }
```
#### 2. Thêm mới một properties
  - Bạn có thể tạo mới một properties và gán giá trị cho nó trên một object đã tồn tại
  ````javascript
person.nationality = "English";
````
  - Ví dụ trên, nếu nationallity properties đã tồn tại, nó sẽ thay đổi giá trị, nếu chưa tồn tại, thì sẽ tạo mới một nationality properties và gán giá trị là English
#### 3.  Deleting Properties
   - Xóa một properties sử dụng từ khóa ```delete```, ví dụ: 
   ```javascript
var person = {firstName: "Thieu", lastName: "Le", age: 18, eyeColor: "blue"};
delete person.age;   // or delete person["age"];
```
#### Object Methods
> Methods là action được thực thi trong đối tượng
> Methods cũng được lưu trữ như một Object properties
 ```javascript
 var person = {
   firstName: "Thieu",
   lastName : "Le",
   id       : 1,
   fullName : function() {
     return this.firstName + " " + this.lastName;
   }
 };
 ```
 - Gọi hàm follow theo cấu trúc ```objectName.methodName()```
 - Ví dụ trên có thể gọi hàm bằng cách ```person.fullName();```
 - Có thể định nghĩa 1 hàm vào object: 
 ```javascript
 person.name = function () {
   return this.firstName + " " + this.lastName;
 };
 ```
 #### Object Accessors (Getter and Setters)
 > Getters and Setters được giới thiệu từ ES5 (ECMAScript 5 (2009))
 > Get and Set cho phép định nghĩa Object Accessors (Computed Properties)
 - Hầu hết các ngôn ngữ lập trình đều có khái niệm get, set. Các hàm này dùng để thiết lập hoặc truy cập giá trị 1 properties của object.
 - Việc sử dụng get, set nhằm đảm bảo các truy cập properties đều phải thông qua hàm get và thiết lập gía trị phải thông qua hàm set
 ```javascript
// Create an object:
var person = {
  firstName: "Thieu",
  lastName : "Le",
  language : "",
  get lang() {
    return this.language;
  },
  set lang(lang) {
      this.language = lang;
  }
};
// Thực hiện hàm set
person.lang = 'en';
// thực hiện hàm get 
const lang = person.lang;
// giá trị của lang lúc này là 'en'
``` 
- Một trong những lợi ích của get, set là bảo mật dữ liệu các thuộc tính. Xem sét ví dụ sau đây :
```javascript
// Create an object:
var person = {
  firstName: "Thieu",
  lastName: "Le",
  t27101986: "en",
  get lang() {
    return this.t27101986.toUpperCase();
  },
  set lang(value) {
      this.t27101986 = value;
  }
};
// Thực hiện việc gán giá trị vào thuộc tính t27101987
// Nhìn bề ngoài sẽ ko biết được thực sự properties tên là gì
person.lang = 'en';
// Display data from the object using a getter:
const lang = person.lang;
// output lang is EN (upper case value)
```
#### Validation with Set 
- Xem set ví dụ dưới đây: 
```javascript
let user = {
  get name() {
    return this._name;
  },

  set name(value) {
    if (value.length < 4) {
      alert("Name is too short, need at least 4 characters");
      return;
    }
    this._name = value;
  }
};

user.name = "Thieu";
alert(user.name); // Thieu

user.name = ""; // Alert "Name is too short, need at least 4 characters"
```
- Ở ví dụ trên, đã check validate value trước khi set data vào thuộc tính _name. Giúp việc kiểm soát đầu vào các object an toàn hơn. 
- Đây là có vẻ là 1 ứng dụng khá hữu ích của get/set nhỉ ?

#### Object.defineProperties
- Ngoài ra, ta cũng có thể định nghĩa get, set thông qua cú pháp ```Object.defineProperties```, 
- Xem set ví dụ sau: 
```javascript
// Define object
var obj = {counter : 0};

// Define setters
Object.defineProperty(obj, "reset", {
  get : function () {this.counter = 0;}
});
Object.defineProperty(obj, "increment", {
  get : function () {this.counter++;}
});
Object.defineProperty(obj, "decrement", {
  get : function () {this.counter--;}
});
Object.defineProperty(obj, "add", {
  set : function (value) {this.counter += value;}
});
Object.defineProperty(obj, "subtract", {
  set : function (value) {this.counter -= value;}
});

// Play with the counter:
obj.reset;
obj.add = 5;
obj.subtract = 1;
obj.increment;
obj.decrement;
```
> Tóm lại, Why Using Getters and Setters?
 - It gives simpler syntax | Cú pháp đơn giản
 - It allows equal syntax for properties and methods | Cú pháp giống như properties và methods 
 - It can secure better data quality | Khả năng bảo mật code
 - It is useful for doing things behind-the-scenes | rất phù hợp phục vụ hậu trường, như validate, hoặc upper case như ví dụ ở trên.
