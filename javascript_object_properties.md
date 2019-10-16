## Thuộc tính của object trong javascript (Object properties)
#### Object Properties
  > Properties are the most important part of any JavaScript object.
 - Properties là những giá trị được gán cho 1 đối tượng trong JS
 - Một Object JS là một tập hợp các properties không sắp xếp
 - Properties có thể thường xuyên được thay đổi, thêm mới, và deleted, nhưng cũng có trường hợp readonly
 ##### 1. Truy cập một Javascript Properties
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
 - 