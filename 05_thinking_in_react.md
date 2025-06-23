### Làm sao để chia giao diện người dùng thành các component hiệu quả?

Tiêu chí:

- Tách biệt logic layout
- Tính tái sử dụng
- Trách nhiệm của component (không nên quá nhiều trách nhiệm)
- Phong cách cá nhân

### Khi nào biết cần chia component?

- Có quá nhiều thứ đang diễn ra trong component (nhiều logic, props)
- Không nên chia nhỏ tất cả mọi thứ sẽ dễ gây nhầm lẫn do có nhiều component có chung công dụng
  => Cân bằng khi chia nhỏ

Đề nghị: Nên xác định rõ thành phần mới nên bao gồm những gì. Chúng ta nên bắt đầu với 1 thành phần tương đối lớn, sau đó chia phần lớn hơn thành các thành phần nhỏ hơn có liên quan khi nó trở nên cần thiết

- Các loại thành phần khác nhau.Có 3 loại:

  - Không trạng thái/ Hoặc hiển thị giao diện :
    - Không states
    - Nhận props sau đó trình bày dữ liệu đó hoặc 1 số nội dung khác, thường là component nhỏ và có khả năng tái sử dụng (logo, text, hiển thị đơn giản)
  - Thành phần có trạng thái:
    - Có states, có khả năng tái sử dụng ( list, card bla..)
  - Thành phần cấu trúc: Trang, bố cục, màn hình … thường là nhiều thành phần nhỏ kết hợp lại với nhau, thành phần này có thể rất lớn và không thể tái sử dụng, nhưng chúng ta không cần nhất thiết phải làm như vậy

- Sự kết hợp các component:
  - Thực chất là việc kết hợp các thành phần khác nhau bằng cách sử dụng props children hoặc bằng các truyền các component là các props
  - Khi kết hợp các component, chúng ta có thể:
    - Tạo ra các thành phần có tính tái sử dụng cao và các thành phần linh hoạt
    - Fix trường hợp 1 component có thể truy cập vào các trạng thái con
    - Cho chúng ta việc để lại các khoảng trống có thể đặt bất cứ thứ gì vào nếu chúng ta muốn
