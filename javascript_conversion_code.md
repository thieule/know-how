## Javascript Coding Conversions
1. Thụt đầu dòng (Indentation)
  - Code không thụt đầu dòng là không thể đọc, đơn giản là như vậy 
 Có thể thụt đầu dòng bằng space white hoặc tab, tôi thường sử dụng tab
  - Khi nào thì cần thụt đầu dòng ? 
    Khi code được quay quanh bằng dấu ngoặc nhọn {...} (curly braces)
2. Dấu ngoặc nhọn (Curly braces)
  - Hầu hêt các cuốn sách để khuyên bạn nên dùng ngoặc nhọn {} trong các trường hợp sử dụng vòng lặp hoặc trong các khối lệnh if else 
  - Tuy nhiên có 1 vài trường hợp cũng có thể không sử dụng {}. 
  ```
    if (msg != '')  alert(msg);
    else  alert('There is no message to show');
  ```  
  - Tóm lại tuỳ trường hợp bạn nên sử dụng hay không, tôi khuyên bạn nếu khối lệnh sau ìf hoặc else có 2 dòng trở lên thì bạn nên dùng {} để code dễ đọc
  
3. Khoảng trắng (White Space)
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
     
## Javascript Naming Conversions
 1. Đặt tên cho hàm khởi tạo.
  - Trong Javascript không có khái niệm class, chỉ có khái niệm hàm khởi tạo.
   Bạn nên viết hoa các chữ cái đầu tiên của mỗi từ trong tên hàm khởi tạo để phân biệt với hàm thông thường.
   ```
    var car = new Car();
    functon Car() {};
    
    var accesser = new DataAccesser();
    function DataAccesser();
```
   >*Cách viết trên được gọi là kiểu PascalCase*
   
  2. Tách từ (Separating Words)
  - Trong trường hợp tên biến hoặc tên hàm thông thường (không phải hàm tạo) ta nên sử dụng kiểu 
    cameCase
    
     
  
  
  Nguồn : https://medium.com/@_jmoller/javascript-conventions-and-best-practices-9e980751c70f
  


