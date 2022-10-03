# Những câu hỏi phỏng vấn Flutter Framework kèm câu trả lời

Đây là một danh sách các câu hỏi phỏng vấn Flutter kèm câu trả lời của chúng

### Ghi chú ###

Những câu trả lời này được tổng hợp từ nhiều nguồn khác nhau như Github, Stackoverflow, Viblo,... dựa trên những câu hỏi từ tài khoản power19942. Nguồn: https://github.com/power19942/flutter-interview-questions

---
  Câu hỏi và trả lời về Flutter Framework
---

1. Sự khác nhau giữa `StatelessWidget` và `StatefullWidget` trong Flutter?

Stateless Widget
Một Stateless Widget không thể thay đổi trạng thái của chúng trong thời gian ứng dụng đang chạy (runtime) có nghĩa là nó không thể tự vẽ lại (redraw) hay tự xây dựng lại (rebuild) khi ứng dụng đang chạy. Stateless Widget là bất biến (immutable).

Statefull Widget
Một Statefull Widget có thể tự vẽ lại nhiều lần trong khi ứng dụng đang chạy có nghĩa là trạng thái của nó có thể thay đổi được. Ví dụ: Khi chúng ta nhấn một nút trong ứng dụng, trạng thái của widget sẽ thay đổi.

---

2. Hãy giải thích về vòng đời của Statefull Widget (`Stateful Widget Lifecycle`)?

Một vòng đời của StatefulWidget bao gồm các bước sau:
createState() -> 
mounted == true -> 
initState() -> 
didChangeDependencies() -> 
build() -> 
didUpdateWidget() -> 
setState() -> 
deactivate() -> 
dispose() -> 
mounted == false

<img src='https://github.com/power19942/flutter-interview-questions/blob/main/img/life_cycle.png' alt="life cycle"/>

Để hiểu rõ hơn về từng trạng thái trong vòng đời của StatefulWidget các bạn hãy click vào link ở bên dưới để tìm hiểu kĩ hơn:
[StatefulWidget Lifecycle](https://viblo.asia/p/flutter-doi-dieu-can-ghi-nho-RQqKLN6zl7z#:~:text=%C4%91%C6%B0%E1%BB%A3c%20t%C3%ADch%20h%E1%BB%A3p.-,StatefulWidget%20Lifecycle,-Khi%20Flutter%20x%C3%A2y)

---

3. Flutter `tree shaking` là gì (Flutter web)?

Khi biên dịch một ứng dụng Flutter web, gói JavaScript được tạo bởi trình biên dịch dart2js. Bản dựng (build) được phát hành có mức độ tối ưu hóa cao nhất, bao gồm cá việc tree shaking mã (code) của bạn. Tree shaking làn quá trình loại bỏ mã chết (dead code) bằng cách chỉ sử dụng đoạn mã (code) mà nó chắc chắn sẽ được thực thi (hay gọi là code chạy được). Điều này có nghĩa là bạn không cần phải lo lắng về kích thước của các thư viện được sử dụng trong ứng dụng của mình vì các lớp (classes) hoặc hàm (function) không sử dụng sẽ bị loại trừ bằng cách biên dịch gói JavaScript.

---

4. Widget `Spacer` là gì?

Spacer quản lý không gian trống giữa các widget với vùng chứa (container) linh hoạt. Kể cả với hàng hay cột chính (Row or Column MainAxis alignment) đều có thể quản lý tốt.

---

5. Sự khác biệt giữa `hot restart` và `hot reload`?

Hot Reload có khả năng tải lại mã (code) của ứng dụng và xây dựng lại (rebuild) widget tree mà không cần khởi động lại. Đồng thời việc nó không chạy lại các hàm main hay initState() sẽ giúp tiết kiệm thời gian và không bị mất trạng thái hiện tại.

Hot Resrart sẽ tải lại toàn bộ thay đổi, khởi động lại ứng dụng Flutter và cũng khởi tạo lại trạng thái ứng ứng dụng.

---

6. Một `InheritedWidget` là gì?

InheritedWidget là một nơi để lưu trữ dữ liệu (data) và cung cấp dữ liệu cho các widget con trong widget tree. Tất cả widget con của InheritedWidget đều có thể truy cập vào nó để lấy dữ liệu. Tức là tự vị trí của InheritedWidget bạn không cần phải truyền dữ liệu xuống từng widget con 1 theo lượt mà widget con có thể ở bất kỳ đâu trong cùng một widget tree cũng có thể truy cập vào dữ liệu và lấy ra dữ liệu mà nó muốn từ InheritedWiget. Hình bên dưới là một ví dụ cho định nghĩa trên:

<img src='https://images.viblo.asia/98e3c9de-5655-4e5a-9311-b7bee943a4d6.PNG' alt="inherited widget"/>

Sử dụng InheriteWidget là một cách quản lý State (State Management) cơ bản, giúp truyền data từ widget tổ tiên (ancestor widget) sang các widget con cháu (descendant widget).
+ Ưu điểm của phương pháp này là rất tiện lợi, nhanh gọn đối với đoạn cây Widget nhỏ (Widget Tree).
+ Nhược điểm của phương pháp này là khi áp dụng vào đoạn widget Tree lớn thì sẽ rất khó kiểm soát và khó triển khai.

---

7. Tại sao phương thức build() trên State mà không phải StatefulWidgets

Lý do chính đằng sau điều này là `StatefulWidget` sử dụng một lớp trạng thái (`State`) riêng biệt mà không xây dựng (build) một phương thức bên trong phần thân của nó. Nó có nghĩa là tất cả các trường bên trong Widget là bất biến và bao gồm tất cả các lớp con của nó.

Mặt khác, `StatelessWidget` có các phương thức xây dựng và liên kết bên trong cơ thể của nó. Đó là do bản chất của `StatelessWidget`, được hiển thị hoàn toàn trên màn hình bằng cách sử dụng thông tin được cung cấp. Nó cũng không cho phép bất kỳ thay đổi nào trong tương lai đối với thông tin `State` của nó.

`StatefulWidget` cho phép chúng tôi thay đổi thông tin `State` trong quá trình sử dụng ứng dụng. Do đó, nó không phù hợp để lưu trữ trong một phương thức xây dựng để thỏa mãn các điều kiện lớp Widget nơi tất cả các trường là bất biến. Đây là lý do chính để giới thiệu `State` . Ở đây, chúng ta chỉ cần ghi đè hàm `createState` để đính kèm `State` đã xác định với `StatefulWidget`, và sau đó tất cả các thay đổi dự kiến sẽ xảy ra trong một lớp riêng biệt.

---

8. Tệp `pubspec.yaml` trong Dart là gì?

Tệp pubspec quản lý nội dung (assets) và các thư viện phụ thuộc (dependencies) của ứng dụng Flutter.

---
