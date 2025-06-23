### Props

- cách truyền dữ liệu giữa các component (cha -> con)
- Giống như 1 tham số truyền vào function
- Props chỉ có thể đọc bên trong component con và update từ component cha

### Luồng dữ liệu 1 chiều

- Truyền từ cha sang con và không ngược lại
- Dễ đoán, dễ hiểu

### Lifting up state

- Data không thể truyền giữa các component cùng cấp
- Lifting up state nghĩa là di chuyển state từ component con lên component cha chung để các component con khác cũng có thể chia sẻ và đồng bộ dữ liệu đó.

Sử dụng:

1. Định nghĩa useState ở component cha (vì nhiều component con cần dùng chung).

2. Truyền giá trị (state) và hàm cập nhật (setState) xuống các component con qua props.

3. Component con có thể gọi setState() để cập nhật dữ liệu.

4. Khi state thay đổi, component cha sẽ re-render, và truyền giá trị mới cho các component con liên quan.

### The key prop

- key là một prop đặc biệt mà React dùng để xác định duy nhất mỗi element trong danh sách.

- Giúp React biết phần tử nào thay đổi / thêm / xóa → từ đó tối ưu việc cập nhật DOM.

#### Tại sao KHÔNG nên dùng index làm key?

- index không đảm bảo tính duy nhất khi danh sách thay đổi theo thứ tự (insert, delete, reorder).

| Trường hợp                     | Nên dùng gì làm `key`                  |
| ------------------------------ | -------------------------------------- |
| Danh sách từ dữ liệu (API, DB) | ID duy nhất từ dữ liệu (`item.id`)     |
| Dữ liệu không có ID            | Tạo UUID, hoặc hash giá trị            |
| Danh sách không thay đổi       | Có thể dùng index tạm thời (ít rủi ro) |
