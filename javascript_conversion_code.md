## Javascript code style guide (AirBnb style)
#### Types
   - 1.1 Biến nguyên thuỷ (Primitives): Khi làm việc với biến nguyên thuỷ, bạn làm việc trực tiếp với giá trị của nó.
        * ```string```
        * ```number```
        * ```boolean```
        * ```null```
        * ```undefined```
        * ```symbol```
   ```gwt javascript
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
   ```gwt javascript
        const foo = [1, 2];

        //Dòng lệnh này gán địa chỉ vùng nhớ của foo cho bar 
        const bar = foo;
        
        bar[0] = 9;
        
        console.log(foo[0], bar[0]); // => 9, 9
        // foo và bar cùng lưu trữ giá trị trên một vùng nhớ, vì vậy khi bar thay đổi, foo cũng thay đổi theo
```
  
## Javascript Coding Conventions
#### Thụt đầu dòng (Indentation)
  - Code không thụt đầu dòng là không thể đọc, đơn giản là như vậy.  Có thể thụt đầu dòng bằng space white hoặc tab, tôi thường sử dụng tab.
  - Khi nào thì cần thụt đầu dòng ? 
    Khi code được quay quanh bằng dấu ngoặc nhọn {...} (curly braces)
#### Dấu ngoặc nhọn (Curly braces)
  - Hầu hêt các cuốn sách để khuyên bạn nên dùng ngoặc nhọn {} trong các trường hợp sử dụng vòng lặp hoặc trong các khối lệnh if else 
  - Tuy nhiên có 1 vài trường hợp cũng có thể không sử dụng {}. 
  ```
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
   ```
    var car = new Car();
    functon Car() {};
    
    var accesser = new DataAccesser();
    function DataAccesser();
```
   >*Cách viết trên được gọi là kiểu PascalCase*
   
  #### Tên hàm thông thường và các biến
  - Trong trường hợp tên biến hoặc tên hàm thông thường (không phải hàm tạo) thì đa số quy ước theo kiểu 
    camelCase
    ```
        // camel case example
        var myAnwesomeFunction = function () {
            var myAnwesomeVariable = 0;  
           // do some thing anwesome ! 
        }
    ```
  #### Tên hằng số 
   - Để phân biệt biến hằng số và biến thông thường thì ta nên đặt tên biến hằng số theo dạng snake_case và in hoa các kí tự.
   ``` 
    // constants example
    var ERROR_CODE_NOT_FOUND = 403;
    var ERROR_CODE_NOT_PERMISSION = 401;
   ```   
  #### Tên hàm hoặc biến private/bublic
   - Biến hoặc hàm private nên sử dụng tiếp đầu ngữ underscore (_)
   ```
   var car = {
     getBrand: function() {
      return this._getModel() + '' + this._getYear();
     },
     _getModel: function() { //... },
     _getYear: function() { //... }
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
  


