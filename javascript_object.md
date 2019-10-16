## Sơ khai về một object trong javascript
#### JavaScript Object
  > Trong Javascript, đối tượng là vua. Nếu bạn hiểu về đối tượng, bạn sẽ hiểu về JavaScript
 - Mọi thứ trong JS đều biểu diễn dưới dạng một đối tượng
    + Booleans, Numbers, String có thể là đối tượng nếu định nghĩa với new từ khóa
    + Dates, Maths, Regular expressions, Arrays, Functions, Objects là đối tượng trong javascript
    + Ngoại trừ biến nguyên thủy (primitives) thì tất cả các giá trị trong javascript đều là 1 đối tượng
 ##### 1. Biến nguyên thủy (Primitives)
   - A primitive là 1 giá trị không có các thuộc tính, không có hàm
   - A primitive data type là dữ liệu có giá trị nguyên thủy
    Javascript định nghĩa 5 loại của kiểu dữ liệu nguyên thủy: 
        + ```String```
        + ```number```
        + ```boolean```
        + ```null```
        + ```undefined```
   
   Các giá trị nguyên thủy là không thể thay đổi (nó được mã hóa cứng, do đó không thể thay đổi)
   > Ví dụ, nếu khai báo biến x = 3.14, lúc này bạn có thể thay đổi giá trị của X, nhưng không thể thay đổi giá trị 3.14
 ##### 2. Biến đối tượng (Object Variables)    
   - Biến trong javascript có thể chứa 1 giá trị đơn
   ```javascript
var person = "Thieu Le Quang"
``` 
   - Nhưng cũng có thể chứa nhiều giá trị trong 1 biến
   ```javascript
   var person = {firstName: 'Thieu', lastName: 'Le', age: 18, eyeColor: 'blue'}
 ```
 => Đây là biến đối tượng
#### 3. Thuộc tính của đối tượng (Object properties)
  Vậy javascript object là 1 biến chứa các biến khác được đặt tên. Các biến được đặt tên trong đối tượng gọi là Object Properties
  > như ví dụ trước, firstName, lastName, age, eyeColor là các object properties của object person
#### 4. Object Methods
 - Object Methods là các action được thực thi trong 1 đối tượng 
 - Object properties có thể chứa các giá trị nguyên thủy (primitive values), các đối tượng khác (other objects), hoặc các (methods) hàm thực thi
```javascript
    var person = {
        firstName: 'Thieu',
        lastName: 'Le',
        age: 18,
        eyeColor: 'blue',
        fullName: function () { 
         return this.firstName + ' ' + this.lastName; 
       }
     }
```
 => Trong ví dụ trên, fullName là một object methods
> JavaScript objects chứa các giá trị được đặt tên (biến), gọi chung là properties và methods.
#### 5. Khởi tạo 1 JS Object
 - Có 4 cách để khởi tạo 1 object trong JS
     * Định nghĩa và khởi tạo 1 single object, sử dụng cách khai báo trực tiếp (object literal)
        ```javascript
        var person = {firstName: 'Thieu', lastName: 'Le', age: 18, eyeColor: 'blue'}
        ```
     * Định nghĩa và khởi tạo 1 single object, sử dụng từ khóa ```new```
        ```javascript
        var person = new Object();
        person.firstName = "Thieu";
        person.lastName = "Le";
        person.age = 18;
        person.eyeColor = "blue";
        ```
     * Định nghĩa 1 object constructor trước, và sau đó tạo objects thông qua constructed type
     ```javascript
        function Person(first, last, age, eye) {
          this.firstName = first;
          this.lastName = last;
          this.age = age;
          this.eyeColor = eye;
        }
       var myFather = new Person("Thieu", "Le", 18, "blue");
    ```
     * Tạo một object thông qua hàm ```Object.create()```
     ```javascript
           const person = {
               fullName: function () { 
                        return this.firstName + ' ' + this.lastName;   
               }
             };
           const me = Object.create(person);
             me.firstName = "Thieu";
             me.lastName = 'Le';
             me.fullName();//print Thieu Le
   ```
     > Trong ECMAScript 5, and object can also be created with the function ```Object.create()```