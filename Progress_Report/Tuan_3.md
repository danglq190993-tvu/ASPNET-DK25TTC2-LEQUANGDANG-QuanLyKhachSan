BÁO CÁO TIẾN ĐỘ ĐỒ ÁN - TUẦN 3
Thời gian thực hiện:** 06/07/2026 - 12/07/2026  
Trọng tâm: Hiện thực hóa code chức năng cốt lõi (Phía Khách hàng)

---

1. Nội dung công việc
- Khởi tạo project và cấu hình chuỗi kết nối Database (Connection String) trong file `Web.config`.
- Triển khai lập trình giao diện và logic xử lý cho phân hệ Khách hàng bao gồm: Màn hình trang chủ, danh sách hiển thị sản phẩm, bộ lọc tìm kiếm nâng cao theo Hãng sản xuất và Nhu cầu sử dụng.
- Xây dựng module Giỏ hàng (chức năng thêm sản phẩm, cập nhật số lượng, xóa sản phẩm khỏi giỏ).
- Thiết lập quy trình Đặt hàng trực tuyến và trang xem lại lịch sử mua hàng của người dùng.

2. Tài liệu liên quan
- Tài liệu kỹ thuật định tuyến URL (ASP.NET Routing) và các loại `ActionResults` trong MVC.
- Phương pháp quản lý và lưu trữ dữ liệu tạm thời bằng cơ chế Session trong ASP.NET nhằm phục vụ tính năng giỏ hàng.

3. Khó khăn gặp phải
- Xử lý đồng bộ dữ liệu giỏ hàng khi người dùng thay đổi số lượng sản phẩm trực tiếp trên giao diện front-end.
- Yêu cầu cập nhật giá trị tức thời mà không được làm tải lại toàn bộ trang (Reload page), đòi hỏi phải áp dụng công nghệ AJAX kết hợp thư viện jQuery.

4. Kết quả đạt được
- Vận hành ổn định toàn bộ luồng nghiệp vụ mua hàng của khách hàng từ bước xem chi tiết sản phẩm, thêm vào giỏ, đặt hàng cho đến khi lưu trữ thành công đơn hàng vào database.
