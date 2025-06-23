## Single Page Application

- xây dựng web mà chỉ chạy trên 1 trang html duy nhất
- người dùng chuyển trang -> trình duyệt không tải lại toàn bộ trang mà chỉ thay đổi nội dung hiển thị bằng JavaScript.
- tốc độ nhanh, mượt mà hơn vì không reload trang liên tục.
- React 1 trong các thư viện có thể tạo ra SPA

## Vấn đề khi xây dựng web bằng vanila js

- Tự viết code để tìm, thêm, xóa, cập nhật DOM
  -> khó đồng bộ data của state mới với state cũ
  -> quá nhiều logic chồng chéo
  -> không cập nhật giao diện hiệu quả
  -> không có kiến trúc rõ ràng nên khó kiểm soát, bảo trì

## React dùng để xây dựng SPA

- app react dc xây dựng dựa trên các component
- component: các build-block tạo nên UI
- UI phức tạo được kết hợp từ nhiều component
