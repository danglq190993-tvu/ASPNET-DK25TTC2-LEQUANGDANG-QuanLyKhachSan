BÁO CÁO TIẾN ĐỘ ĐỒ ÁN - TUẦN 4
Thời gian thực hiện: 13/07/2026 - 19/07/2026  
Trọng tâm: Hiện thực hóa code chức năng quản trị (Phía Admin) và bổ sung tính năng cải tiến

1. Nội dung công việc
- Tích hợp thành công giao diện quản trị SB Admin 2 vào cấu trúc thư mục của phân hệ Admin Area.
- Viết mã nguồn xử lý các chức năng CRUD (Create, Read, Update, Delete) cho các thực thể hệ thống: Quản lý thông tin sản phẩm (Laptop), Quản lý thể loại, Quản lý danh sách đơn hàng và Quản lý chuyên mục bài viết tin tức.
- Thiết lập giao diện quản lý vai trò người dùng (Role Management) và cơ chế phân quyền truy cập.

2. Tài liệu liên quan
- Tài liệu lập trình nâng cao với ASP.NET Identity.
- Cơ chế phân quyền và kiểm soát truy cập dựa trên vai trò người dùng (Role-based Authorization) giữa tài khoản Admin và Khách hàng thông thường.

3. Khó khăn khi viết thêm chức năng
- Gặp trở ngại lớn khi nghiên cứu tích hợp các tính năng nâng cao theo đề xuất cải tiến đề tài bao gồm việc thiết lập hệ thống thông báo nổi (Toast Notification) thời gian thực mỗi khi hệ thống ghi nhận có đơn đặt hàng mới.
- Khó khăn trong việc xây dựng logic gợi ý thông minh tự động kiểm tra trùng khớp thông tin khách hàng cũ dựa trên số điện thoại/email để đưa ra đề xuất tạo mới hoặc liên kết profile khách hàng tại trang Admin.
- Việc thử nghiệm cấu hình Realtime tiêu tốn nhiều thời gian cấu hình hệ thống nhưng hiệu quả chưa đạt như mong muốn.

4. Kết quả đạt được
- Hoàn thiện toàn bộ các màn hình hiển thị và tính năng CRUD phía quản trị Admin.
- Tích hợp thành công bộ lọc phân quyền cơ bản (Authorize Attribute) giúp chặn truy cập trái phép vào các liên kết nội bộ của Admin.
