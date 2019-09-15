## Javascript code style guide (AirBnb style)
#### Types
   - 1.1 Biến nguyên thuỷ (Primitives): Khi làm việc với biến nguyên thuỷ, bạn làm việc trực tiếp với giá trị của nó.
        * ```string```
        * ```number```
        * ```boolean```
        * ```null```
        * ```undefined```
        * ```symbol```
   ```javascript
        const foo = 1;
        // Dòng lệnh này khởi tạo vùng nhớ mới cho bar, vùng nhớ này dược lưu trữ giá trị copy từ foo
        let bar = foo;
        
        bar = 9;
        
        console.log(foo, bar); // => 1, 9
        // foo và bar lưu trữ giá trị trên 2 vùng nhớ khác nhau, vì vậy khi bar thay đổi, foo cũng thay đổi theo
``` 
   - 1.2 Kiểu phức tạp (Complex): Khi làm việc với loại biến này, bạn làm việc trên một tham chiếu (địa chỉ) đến giá trị của nó.
        * ```object```
        * ```array```
        * ```function```
   ```javascript
        const foo = [1, 2];

        //Dòng lệnh này gán địa chỉ vùng nhớ của foo cho bar 
        const bar = foo;
        
        bar[0] = 9;
        
        console.log(foo[0], bar[0]); // => 9, 9
        // foo và bar cùng lưu trữ giá trị trên một vùng nhớ, vì vậy khi bar thay đổi, foo cũng thay đổi theo
```
#### References
   - Hằng số (Const)
   ```javascript
// bad
var a = 1;
var b = 2;

// good
const a = 1;
const b = 2;
//việc định nghĩa hằng số theo từ khoá const sẽ đảm bảo các hằng số không được gán lại giá trị khác.  
```
   - Khai báo biến với let
    Từ ES6 trở đi sẽ thêm vào cách khai báo biến mới let, let khác với var ở scope hoạt động 
      * const và let chỉ tồn tại giá trị trong phạm vi block code  {}, ra ngoài block này sẽ bị xoá
      * var sẽ tồn tại xuyên xuốt function chứa nó.
   - Eslint rule sẽ ngăn bạn sử dụng var [no-var](https://eslint.org/docs/rules/no-var.html), chỉ nên sử dụng let
#### Objects
   - Khởi tạo object thông qua {} thay vì new Object(). Eslint: [no-new-object](https://eslint.org/docs/rules/no-new-object.html)
     ```javascript
      // bad
      const item = new Object();
      
      // good
      const item = {};
      ```
   - Khai báo các thuộc tính trong 1 khu vực, kể cả thuộc tính động 
   ```javascript
       function getKey(k) {
         return `a key named ${k}`;
       }
       
       // bad
       const obj = {
         id: 5,
         name: 'San Francisco',
       };
       obj[getKey('enabled')] = true;
       
       // good
       const obj = {
         id: 5,
         name: 'San Francisco',
         [getKey('enabled')]: true,
       };
   ```   
   - Khai báo hàm rút gọn trong object. eslint: [object-shorthand](https://eslint.org/docs/rules/object-shorthand.html)
   ```javascript
       // bad
       const atom = {
         value: 1,
       
         addValue: function (value) {
           return atom.value + value;
         },
       };
       
       // good
       const atom = {
         value: 1,
       
         addValue(value) {
           return atom.value + value;
         },
       };
   ```
   - Khai báo thuộc tính ngắn gọn
   ```javascript
        const lukeSkywalker = 'Luke Skywalker';
        
        // bad
        const obj = {
          lukeSkywalker: lukeSkywalker,
        };
        
        // good
        const obj = {
          lukeSkywalker,
        };
   ```
   - Nhóm các thuộc tính khai báo ngắn lên đầu tiên của Object
   ```javascript
       const anakinSkywalker = 'Anakin Skywalker';
       const lukeSkywalker = 'Luke Skywalker';
       
       // bad
       const obj = {
         episodeOne: 1,
         twoJediWalkIntoACantina: 2,
         lukeSkywalker,
         episodeThree: 3,
         mayTheFourth: 4,
         anakinSkywalker,
       };
       
       // good
       const obj = {
         lukeSkywalker,
         anakinSkywalker,
         episodeOne: 1,
         twoJediWalkIntoACantina: 2,
         episodeThree: 3,
         mayTheFourth: 4,
       };
   ```
   - Chỉ quote các thuộc tính có định danh không hợp lệ. Eslint: [quote-props](https://eslint.org/docs/rules/quote-props.html)
   ```javascript
       // bad
       const bad = {
         'foo': 3,
         'bar': 4,
         'data-blah': 5,
       };
       
       // good
       const good = {
         foo: 3,
         bar: 4,
         'data-blah': 5,
       };
   ```
   - Không gọi các hàm Object.prototype trực tiếp như các hàm ```hasOwnProperty```, ```propertyIsEnumerable```, và ```isPrototypeOf```. eslint: [no-prototype-builtins](https://eslint.org/docs/rules/no-prototype-builtins)
        > Vì các hàm này có thể cùng tên với các thuộc tính của object hoặc object này có thể là null (```Object.create(null)```)
   ```javascript
       // bad
       console.log(object.hasOwnProperty(key));
       
       // good
       console.log(Object.prototype.hasOwnProperty.call(object, key));
       
       // best
       const has = Object.prototype.hasOwnProperty; // cache the lookup once, in module scope.
       console.log(has.call(object, key));
       /* or */
       import has from 'has'; // https://www.npmjs.com/package/has
       console.log(has(object, key));
   ```
#### Arrays
   - Khởi tạo object thông qua [] thay vì new Array(). Eslint: [no-array-constructor](https://eslint.org/docs/rules/no-array-constructor.html)
   ```javascript
         // bad
         const item = new Array();
         
         // good
         const item = [];
  ```
   - Thêm một phần tử vào cuối mảng
   ```javascript
   const someStack = [];
   
   // bad
   someStack[someStack.length] = 'abracadabra';
   
   // good
   someStack.push('abracadabra');
   ```
   - Sử dụng ... để copy Array
   ```javascript
   // bad
   const len = items.length;
   const itemsCopy = [];
   let i;
   
   for (i = 0; i < len; i += 1) {
     itemsCopy[i] = items[i];
   }
   
   // good
   const itemsCopy = [...items];
   ```
   - Copy một iterable Object to an Array, sử dụng ... thay vì ```Array.from```.
   ```javascript
   const foo = document.querySelectorAll('.foo');
   
   // good
   const nodes = Array.from(foo);
   
   // best
   const nodes = [...foo]; 
   ```
   - Sử dụng ```Array.from``` để convert từ một array-like object thành một array
   ```javascript
   const arrLike = { 0: 'foo', 1: 'bar', 2: 'baz', length: 3 };
   
   // bad
   const arr = Array.prototype.slice.call(arrLike);
   
   // good
   const arr = Array.from(arrLike);
   ```
   - Sử dụng return trong định nghĩa các array method callback, eslint: [array-callback-return](https://eslint.org/docs/rules/array-callback-return) 
   ```javascript
   // good
   [1, 2, 3].map((x) => {
     const y = x + 1;
     return x * y;
   });
   
   // good
   [1, 2, 3].map((x) => x + 1);
   
   // bad - no returned value means `acc` becomes undefined after the first iteration
   [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
     const flatten = acc.concat(item);
   });
   
   // good
   [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
     const flatten = acc.concat(item);
     return flatten;
   });
   
   // bad
   inbox.filter((msg) => {
     const { subject, author } = msg;
     if (subject === 'Mockingbird') {
       return author === 'Harper Lee';
     } else {
       return false;
     }
   });
   
   // good
   inbox.filter((msg) => {
     const { subject, author } = msg;
     if (subject === 'Mockingbird') {
       return author === 'Harper Lee';
     }
   
     return false;
   });
   ```
   - Xuống dòng sau khi mở và trước khi đóng ngoặc nếu một mảng có nhiều dòng
   ```javascript
   // bad
   const arr = [
     [0, 1], [2, 3], [4, 5],
   ];
   
   const objectInArray = [{
     id: 1,
   }, {
     id: 2,
   }];
   
   const numberInArray = [
     1, 2,
   ];
   
   // good
   const arr = [[0, 1], [2, 3], [4, 5]];
   
   const objectInArray = [
     {
       id: 1,
     },
     {
       id: 2,
     },
   ];
   
   const numberInArray = [
     1,
     2,
   ];
   ```
#### Destructuring
   > Destructuring là chức năng mới có từ javascript ES6, Giúp truy vấn dữ liệu từ Array hoặc Object và gán chúng vào các biến thông thường. Tuy nhiên, việc "lấy ra dữ liệu" này sẽ chỉ copy mà không làm thay đổi cấu trúc của Object hoặc Array.
   - Sử dụng Destructuring khi truy cập và sử dụng nhiều thuộc tính của một đối tượng. Eslint: [prefer-destructuring](https://eslint.org/docs/rules/prefer-destructuring)
   > Tại sao ? Vì sử dụng Destructuring sẽ tiết kiệm bộ nhớ cho việc tạo tham chiếu tạm đến các thuộc tính đó.
   ```javasctript
   // bad
   function getFullName(user) {
     const firstName = user.firstName;
     const lastName = user.lastName;
   
     return `${firstName} ${lastName}`;
   }
   
   // good
   function getFullName(user) {
     const { firstName, lastName } = user;
     return `${firstName} ${lastName}`;
   }
   
   // best
   function getFullName({ firstName, lastName }) {
     return `${firstName} ${lastName}`;
   }
   ```
   - Sử dụng Array Destructuring. Eslint: [prefer-destructuring](https://eslint.org/docs/rules/prefer-destructuring)   
   ```javascript
   const arr = [1, 2, 3, 4];
   
   // bad
   const first = arr[0];
   const second = arr[1];
   
   // good
   const [first, second] = arr;
   ```
   - Sử dụng Object Destructuring với nhiều giá trị trả vê. Không sử dụng Array Destructuring.
   > Tại sao ? Vì bạn có thể thêm thuộc tính mới hoặc thay đổi vị trí mà không làm phát sinh lỗi
   ```javascript 
   // bad
   function processInput(input) {
     // then a miracle occurs
     return [left, right, top, bottom];
   }
   
   // the caller needs to think about the order of return data
   const [left, __, top] = processInput(input);
   
   // good
   function processInput(input) {
     // then a miracle occurs
     return { left, right, top, bottom };
   }
   
   // the caller selects only the data they need
   const { left, top } = processInput(input);
   ```
#### Strings
   - Sự dụng dấu ngoặc đơn ```''``` trong chuỗi. Eslint: [quotes](https://eslint.org/docs/rules/quotes.html)
   ```javascript
   // bad
   const name = "Capt. Janeway";
   
   // bad - template literals should contain interpolation or newlines
   const name = `Capt. Janeway`;
   
   // good
   const name = 'Capt. Janeway';
   ``` 
   - Nếu một chuỗi hơn 100 ký tự, không nên viết xuống dòng sử dụng ký tự nối chuỗi
   ```javascript
   // bad
   const errorMessage = 'This is a super long error that was thrown because \
   of Batman. When you stop to think about how Batman had anything to do \
   with this, you would get nowhere \
   fast.';
   
   // bad
   const errorMessage = 'This is a super long error that was thrown because ' +
     'of Batman. When you stop to think about how Batman had anything to do ' +
     'with this, you would get nowhere fast.';
   
   // good
   const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
   ```
   - Khi build một chuỗi có tham số, hạn chế việc nối chuỗi thay vào đó sử dụng format hoặc template. Eslint [prefer-template](https://eslint.org/docs/rules/prefer-template.html), [template-curly-spacing](https://eslint.org/docs/rules/template-curly-spacing)
   > Tại sao ? Tạo template khiến chuỗi ngắn gọn và dễ đọc hơn. Việc sử maintain sau này cũng dễ dàng hơn.  
  ```javascript
  // bad
  function sayHi(name) {
    return 'How are you, ' + name + '?';
  }
  
  // bad
  function sayHi(name) {
    return ['How are you, ', name, '?'].join();
  }
  
  // bad
  function sayHi(name) {
    return `How are you, ${ name }?`;
  }
  
  // good
  function sayHi(name) {
    return `How are you, ${name}?`;
  }
  ```
  - Không bao giờ được sử dụng eval() trong 1 chuỗi, Nó tạo ra nhiều lỗ hỏng bảo mật. eslint: [no-eval](https://eslint.org/docs/rules/no-eval)
  - Không cần thiết Escape các ký tự trong chuỗi. Eslint: [no-useless-escape](https://eslint.org/docs/rules/no-useless-escape)
  > Tại sao ?, vì dấu '\\' sẽ khiến chuỗi khó đọc hơn. Chỉ nên sử dụng khi cần thiết.
  ```javascript
  // bad
  const foo = '\'this\' \i\s \"quoted\"';
  
  // good
  const foo = '\'this\' is "quoted"';
  const foo = `my name is '${name}'`;
  ``` 
  - Sử dụng cách định nghĩa hàm theo biểu thức thay vì định nghĩa hàm. Eslint: [func-style](https://eslint.org/docs/rules/func-style)
  > Tại sao? Tất cả các khai  báo hàm được đưa lên trên cùng, vì thế trong javascript ta có thể gọi hàm trước khi định nghĩa, điều này gây khó đọc và khó mở rộng sau này.
  Trường hợp một hàm có lượng dòng lớn hoặc phức tạp, bạn nên để ra một file riêng như định nghĩa một module.
  ```javascript
  // bad
  function foo() {
    // ...
  }
  
  // bad
  const foo = function () {
    // ...
  };
  
  // good
  // lexical name distinguished from the variable-referenced invocation(s)
  const short = function longUniqueMoreDescriptiveLexicalFoo() {
    // ...
  };
  ```
  - Đóng gói hàm sử dụng ngay trong một dấu ngoặc (IIFE - immediately-invoked function expression)[wrap-iife](https://eslint.org/docs/rules/wrap-iife.html)
  > Tại sao ? IIFE là khởi tạo 1 function và thực thi nó ngay lập tức. Vậy tại sao lại dùng IIFE? Bởi vì IIFE như là một các hộp đóng gói code của chính nó. Do đó, những biến trong hộp này là private, bên ngoài(global) không thể truy xuất hay thay đổi được. Và nếu vô tình bạn đặt tên biến giống với global thì cũng không bị ảnh hưởng bên ngoài.
  IFE hữu ích khi chúng ta muốn đóng gói code để nó không ảnh hưởng đến các biến toàn cục. Nó hữu ích khi chúng ta viết những thư viện. Sau đó, chúng ta nhúng vào những trang web khác nhau thì cũng không ảnh hưởng đến code của chúng ta.
  ```javascript
  // immediately-invoked function expression (IIFE)
  (function () {
    console.log('Welcome to the Internet. Please follow me.');
  }());
```
- Không khai báo 1 hàm trong 1 non-function block (if, while, etc), trong trường hợp này ta assign hàm như 1 biến. Eslint: [no-loop-func](https://eslint.org/docs/rules/no-loop-func.html)
```javascript
// bad
if (currentUser) {
  function test() {
    console.log('Nope.');
  }
}

// good
let test;
if (currentUser) {
  test = () => {
    console.log('Yup.');
  };
}
```
- Không đặt tên biến tham số arguments. Sẽ bị trùng với biến arguments của hàm, và triệt tiêu biến này.
```javascript
// bad
function foo(name, options, arguments) {
  // ...
}

// good
function foo(name, options, args) {
  // ...
}
```
Never use arguments, sử dụng cú pháp ... thay thế. [prefer-rest-params](https://eslint.org/docs/rules/prefer-rest-params)
```javascript
// bad
function concatenateAll() {
  const args = Array.prototype.slice.call(arguments);
  return args.join('');
}

// good
function concatenateAll(...args) {
  return args.join('');
}
```
- Use cú pháp tham số mặc định của hàm, thay vì gán mặc định trong hàm.
```javascript
// really bad
function handleThings(opts) {
  // No! We shouldn’t mutate function arguments.
  // Double bad: if opts is falsy it'll be set to an object which may
  // be what you want but it can introduce subtle bugs.
  opts = opts || {};
  // ...
}

// still bad
function handleThings(opts) {
  if (opts === void 0) {
    opts = {};
  }
  // ...
}

// good
function handleThings(opts = {}) {
  // ...
}
```
- Không sử dụng tham số mặc định có ảnh hưởng phụ không kiểm soát được.
```javascript
var b = 1;
// bad
function count(a = b++) {
  console.log(a);
}
count();  // 1
count();  // 2
count(3); // 3
count();  // 3
```
- Luôn khai báo biến hàm có giá trị mặc định sau cùng.
```javascript
// bad
function handleThings(opts = {}, name) {
  // ...
}

// good
function handleThings(name, opts = {}) {
  // ...
}
```
- Không sử dụng Function hàm dựng  để tạo mới 1 function. [no-new-func](https://eslint.org/docs/rules/no-new-func)
> Tại sao? tạo một hàm như này cũng giống như sửa dụng eval() mở ra các lỗ hỏng.
```javasript
// bad
var add = new Function('a', 'b', 'return a + b');

// still bad
var subtract = Function('a', 'b', 'return a - b');
```
- Không thay đổi giá trị hoặc gán lại giá trị của biến tham số của hàm. [no-param-reassign](https://eslint.org/docs/rules/no-param-reassign.html)
```javascript
// bad
function f1(obj) {
  obj.key = 1;
}

// good
function f2(obj) {
  const key = Object.prototype.hasOwnProperty.call(obj, 'key') ? obj.key : 1;
}
```
```javascript
// bad
function f1(a) {
  a = 1;
  // ...
}

function f2(a) {
  if (!a) { a = 1; }
  // ...
}

// good
function f3(a) {
  const b = a || 1;
  // ...
}

function f4(a = 1) {
  // ...
}
```

## Javascript Coding Conventions
#### Thụt đầu dòng (Indentation)
  - Code không thụt đầu dòng là không thể đọc, đơn giản là như vậy.  Có thể thụt đầu dòng bằng space white hoặc tab, tôi thường sử dụng tab.
  - Khi nào thì cần thụt đầu dòng ? 
    Khi code được quay quanh bằng dấu ngoặc nhọn {...} (curly braces)
#### Dấu ngoặc nhọn (Curly braces)
  - Hầu hêt các cuốn sách để khuyên bạn nên dùng ngoặc nhọn {} trong các trường hợp sử dụng vòng lặp hoặc trong các khối lệnh if else 
  - Tuy nhiên có 1 vài trường hợp cũng có thể không sử dụng {}. 
  ```javascript
    if (msg != '')  alert(msg);
    else  alert('There is no message to show');
  ```  
  - Tóm lại tuỳ trường hợp bạn nên sử dụng hay không, tôi khuyên bạn nếu khối lệnh sau ìf hoặc else có 2 dòng trở lên thì bạn nên dùng {} để code dễ đọc
  
#### Khoảng trắng (White Space)
  - Khoảng trắng góp phần làm tăng khả năng dễ đọc (readability) và tính nhất quán (consistency)
  - Một vài trường hợp nên dùng khoảng trắng: 
     * Sau dấu chấm phấy (;) tách các phần của for. 
      ```vd: for(i = 0; i <= 20; i++) {} ```
     * Sau các dấu phấy (,) phân tách các phần tử trong mảng
     ```vd: var array = [1, 2, 4, 10];```
       
     * Sau các dấu phẩy (,) phân tách các giá trị của thuộc tính đối tượng và sau dấu hai chấm (:) phân cách tên thuộc tính và giá trị của chúng.
     	```vd: var object = {id: 20, name: 'thieu'};```
     * Sau dấu phấy (,) phân chia các tham số của hàm, ```ví dụ: fn(a, b, c)```
     * Trước dấu ngoặc nhọn {, trong định nghĩa hàm: ```vd: function fn() {};```
     * Sau từ khoá function trong biểu thức khai báo hàm ẩn danh (anonymous), ```vd: var fn = function () {};```
     * Trước khi mở các ngoặc nhọn mở { trong định nghĩa hàm, khối lệnh if else, vòng lặp (for) và trong câu lệnh khai báo đối tượng.
     * Sau ngoặc nhọn đóng và else hoặc white 
     * Giữa các toán tử, ```vd: if (a == b) {}; var a = 1;```
     
## Javascript Naming Conventions
 #### Đặt tên cho hàm khởi tạo.
  - Trong Javascript không có khái niệm class, chỉ có khái niệm hàm khởi tạo.
   Bạn nên viết hoa các chữ cái đầu tiên của mỗi từ trong tên hàm khởi tạo để phân biệt với hàm thông thường.
   ```javascript
    var car = new Car();
    function Car() {};
    
    var accesser = new DataAccesser();
    function DataAccesser() {};
```
   >*Cách viết trên được gọi là kiểu PascalCase*
   
  #### Tên hàm thông thường và các biến
  - Trong trường hợp tên biến hoặc tên hàm thông thường (không phải hàm tạo) thì đa số quy ước theo kiểu 
    camelCase
    ```javascript
        // camel case example
        var myAnwesomeFunction = function () {
            var myAnwesomeVariable = 0;  
           // do some thing anwesome ! 
        }
    ```
  #### Tên hằng số 
   - Để phân biệt biến hằng số và biến thông thường thì ta nên đặt tên biến hằng số theo dạng snake_case và in hoa các kí tự.
   ```javascript
    // constants example
    const ERROR_CODE_NOT_FOUND = 403;
    const ERROR_CODE_NOT_PERMISSION = 401;
   ```   
  #### Tên hàm hoặc biến private/public
   - Biến hoặc hàm private nên sử dụng tiếp đầu ngữ underscore (_)
   ```javascript
   var car = {
     getBrand: function() {
      return this._getModel() + '' + this._getYear();
     },
     _getModel: function() { },
     _getYear: function() { }
    }
   ```
   - Trong Javascript không có khái niệm hàm private, tất cả đều là public. 
   - Tuy nhiên để tường minh ta vẫn nên sử dụng underscore prefix vào các hàm mà không nên gọi từ bên ngoài đối tượng.
  #### Viết comments 
   - Viết comment giúp người khác hoặc bạn hiểu về code của bạn đã viết. 
   - Viết comment cũng là 1 cách tốt để bổ sung thông tin về hàm của bạn đã định nghĩa. 
   - Tuy nhiên bạn cũng không nên quá nhiệt tình viết comment cho từng dòng.
   - Chỉ đối với những thuật toán khó hiểu, hoặc bạn cần để lại lưu ý gì cho người sau sử dụng code của bạn. 
   - Vì theo thời gian các dòng code của bạn bị thay đổi, những dòng comment từng dòng đó cũng không còn ý nghĩa.
   - Một ví dụ về comment code đầu hàm : 
   ``` 
   /**
   * My method description.  Like other pieces of your comment blocks, 
   * this can span multiple lines.
   *
   * @method methodName
   * @param {String} foo Argument 1
   * @param {Object} config A config object
   * @param {String} config.name The name on the config object
   * @param {Function} config.callback A callback function on the config object
   * @param {Boolean} [extra=false] Do extra, optional work
   * @return {Boolean} Returns true on success
   */
   ```
   - Để việc comment thực hiện nhanh chóng, bạn có thể sử dụng tool YUIDOC: https://yui.github.io/yuidoc/
     
  ## Kết luận
  - Tất cả các quy tắc đặt ra đều giúp bạn và team phát triển của bạn làm việc thống nhất.
  - Các quy tắc giúp code của bạn sáng hơn, chuyên nghiệp hơn. 
  - Các quy tắc cũng giúp code của bạn dễ đọc, dễ bảo dưỡng và mở rộng sau này.
  - Các quy tắc giúp hạn chế bug phát sinh tối thiểu.
  - Để là một người lập trình chuyên nghiệp, việc đầu tiên bạn phải chăm chút đó là code của mình.
     
     
  Nguồn tham khảo: https://medium.com/@_jmoller/javascript-conventions-and-best-practices-9e980751c70f
  https://github.com/airbnb/javascript#references


