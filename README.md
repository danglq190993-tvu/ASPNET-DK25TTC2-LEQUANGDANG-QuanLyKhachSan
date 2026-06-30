# Hotel Book - Hệ Thống Quản Lý Khách Sạn

## Mục lục
- [Giới thiệu](#giới-thiệu)
- [Công nghệ sử dụng](#công-nghệ-sử-dụng)
- [Cấu trúc đồ án](#cấu-trúc-đồ-án)
- [Hướng dẫn cài đặt](#hướng-dẫn-cài-đặt)
  - [Bước 1: Import database vào SSMS](#bước-1-import-database-vào-ssms)
  - [Bước 2: Mở project bằng Visual Studio](#bước-2-mở-project-bằng-visual-studio)
  - [Bước 3: Cấu hình Web.config](#bước-3-cấu-hình-webconfig)
  - [Bước 4: Chạy project](#bước-4-chạy-project)
- [Tài khoản đăng nhập](#tài-khoản-đăng-nhập)
- [Các chức năng của đồ án](#các-chức-năng-của-đồ-án)
  - [Trang khách hàng (Public)](#trang-khách-hàng-public)
  - [Trang quản trị (Admin)](#trang-quản-trị-admin)
- [Map đồ án](#map-đồ-án)
- [Các lỗi thường gặp và cách sửa](#các-lỗi-thường-gặp-và-cách-sửa)

---

## Giới thiệu

**Hotel Book** là hệ thống quản lý khách sạn được xây dựng bằng **ASP.NET MVC 5** kết hợp **Entity Framework 6** (Code First) và **SQL Server**. Hệ thống gồm hai phần chính: **trang khách hàng** (Public) cho phép khách hàng xem phòng, đặt phòng, đánh giá và **trang quản trị** (Admin) dành cho nhân viên/quản lý quản lý phòng, dịch vụ, đơn đặt phòng và người dùng.

---

## Công nghệ sử dụng

| Layer | Công nghệ |
|-------|-----------|
| Frontend | HTML5, CSS3, Bootstrap 4, JavaScript/jQuery, CKEditor |
| Backend | ASP.NET MVC 5 (.NET Framework 4.7.2) |
| ORM | Entity Framework 6 (Code First) |
| Database | Microsoft SQL Server |
| Biểu đồ | Chart.js |
| Thanh toán | MoMo Payment Gateway (test) |
| Email | SMTP Gmail |

---

## Cấu trúc đồ án

```
DamManhLinh/
├── src/
│   ├── quanlykhachsan.sln                 # Solution file
│   └── QuanLyKhachSan/
│       ├── App_Start/                     # Cấu hình khởi tạo
│       │   ├── BundleConfig.cs            # Bundling script/style
│       │   ├── FilterConfig.cs           # Global filters
│       │   └── RouteConfig.cs            # Định tuyến URL
│       ├── Content/                       # Tài nguyên tĩnh
│       │   ├── Admin/                    # CSS/JS cho trang admin
│       │   ├── css/                      # CSS cho trang public
│       │   ├── ckeditor/                 # Rich text editor
│       │   ├── fonts/                    # Font icons
│       │   ├── images/                   # Hình ảnh phòng, khách sạn
│       │   └── js/                       # JavaScript public
│       ├── Controllers/                  # Bộ điều khiển
│       │   ├── Admin/                    # Controller quản trị
│       │   │   ├── AdminAuthenticationController.cs
│       │   │   ├── AdminBookingController.cs
│       │   │   ├── AdminHomeController.cs
│       │   │   ├── AdminModulesController.cs
│       │   │   ├── AdminRoomController.cs
│       │   │   ├── AdminServiceController.cs
│       │   │   ├── AdminTypeController.cs
│       │   │   └── AdminUserController.cs
│       │   └── Public/                   # Controller khách hàng
│       │       ├── PublicAuthenticationController.cs
│       │       ├── PublicBookingController.cs
│       │       ├── PublicHomeController.cs
│       │       ├── PublicModulesController.cs
│       │       ├── PublicRoomController.cs
│       │       └── PublicUserController.cs
│       ├── Daos/                         # Lớp truy xuất dữ liệu
│       │   ├── BookingDao.cs
│       │   ├── BookingServiceDao.cs
│       │   ├── RoomCommentDao.cs
│       │   ├── RoomDao.cs
│       │   ├── ServiceDao.cs
│       │   ├── TypeDao.cs
│       │   └── UserDao.cs
│       ├── Models/                       # Mô hình dữ liệu
│       │   ├── Booking.cs
│       │   ├── BookingService.cs
│       │   ├── QuanLyKhachSanDBContext.cs
│       │   ├── Role.cs
│       │   ├── Room.cs
│       │   ├── RoomComment.cs
│       │   ├── Service.cs
│       │   ├── Type.cs
│       │   └── User.cs
│       ├── Migrations/                   # Lịch sử migration EF
│       ├── Views/                        # Giao diện Razor
│       │   ├── AdminAuthentication/
│       │   ├── AdminBooking/
│       │   ├── AdminHome/
│       │   ├── AdminModules/
│       │   ├── AdminRoom/
│       │   ├── AdminService/
│       │   ├── AdminType/
│       │   ├── AdminUser/
│       │   ├── PublicAuthentication/
│       │   ├── PublicBooking/
│       │   ├── PublicHome/
│       │   ├── PublicModules/
│       │   ├── PublicRoom/
│       │   ├── PublicUser/
│       │   └── Shared/
│       ├── Global.asax / Global.asax.cs
│       ├── Web.config                     # Cấu hình ứng dụng
│       ├── quanlykhachsan.csproj
│       └── packages.config
├── scriptDML.sql                         # Script tạo database
└── README.md
```

---

## Hướng dẫn cài đặt

### Bước 1: Import database vào SSMS

1. Mở **SQL Server Management Studio (SSMS)**.
2. Kết nối đến server của bạn.
3. Mở file `scriptDML.sql` trong SSMS:
   - Menu **File** → **Open** → **File** → chọn `scriptDML.sql`
   - Hoặc nhấn `Ctrl + O` rồi duyệt đến file.
4. Nhấn **Execute** (`F5`) hoặc nhấn nút **! Execute** trên toolbar.
5. Kiểm tra database đã được tạo:
   - Trong **Object Explorer**, click chuột phải vào **Databases** → **Refresh**.
   - Xác nhận database `DBQuanLyKhachSan` xuất hiện.

> **Lưu ý:** Nếu database đã tồn tại, xóa database cũ trước bằng lệnh `DROP DATABASE DBQuanLyKhachSan;` hoặc xóa qua SSMS.

### Bước 2: Mở project bằng Visual Studio

1. Mở thư mục `D:\tvu-Project\Q.Dang\DamManhLinh\src\`.
2. Double-click vào file **`quanlykhachsan.sln`** để mở project trong Visual Studio.
3. Đợi Visual Studio restore NuGet packages (nếu có thông báo).

### Bước 3: Cấu hình Web.config

Mở file `QuanLyKhachSan/Web.config`, tìm phần `<connectionStrings>` và sửa cho đúng với SQL Server của bạn:

```xml
<connectionStrings>
  <add name="DBConnectionString"
       connectionString="Data Source=YOUR_SERVER_NAME\SQLEXPRESS01;Database=DBQuanLyKhachSan;Integrated Security=True"
       providerName="System.Data.SqlClient" />
</connectionStrings>
```

- **`YOUR_SERVER_NAME`**: Thay bằng tên server SQL của bạn (xem trong SSMS, Object Explorer, phần Server Name, ví dụ: `DESKTOP-XXXX`, `localhost`, `.`).
- **`SQLEXPRESS01`**: Thay bằng tên instance SQL Server của bạn (nếu dùng SQL Server đầy đủ không có instance, chỉ cần `.` hoặc `(local)`).

#### Cấu hình email (nếu cần gửi OTP/quen mat khau):

```xml
<appSettings>
  <add key="FormEmailAddress" value="your_email@gmail.com" />
  <add key="FormEmailPassword" value="your_app_password" />
  <add key="SMTPHost" value="smtp.gmail.com" />
  <add key="SMTPPort" value="587" />
  <add key="EnabledSSL" value="true" />
</appSettings>
```

> **Cách lấy App Password Gmail:** Bật xác minh 2 bước → Vào **Google Account** → **Security** → **App passwords** → Tạo app password mới cho "Mail".

### Bước 4: Chạy project

1. Trong Visual Studio, nhấn **`F5`** hoặc click nút **IIS Express** (màu xanh lá).
2. Trình duyệt sẽ mở trang chủ tại `https://localhost:44385/`.
3. Đăng nhập bằng tài khoản admin để vào trang quản trị.

---

## Tài khoản đăng nhập

### Tài khoản Admin (Quản trị viên)

| Thông tin | Giá trị |
|-----------|---------|
| **Username** | `admin` |
| **Password** | `admin123` |

> Truy cập trang đăng nhập admin: `/AdminAuthentication/Login`

### Các tài khoản mặc định khác

| ID | Username | Họ tên | Vai trò | Password |
|----|----------|--------|---------|---------|
| 1 | quanlykhachsan | Đàm Mạnh Linh | Khách hàng (idRole=3) | `123456789` |
| 2 | admin | Quản trị viên | Admin (idRole=1) | `admin123` |
| 3 | nguyenviena | Nguyễn Viên A | Nhân viên (idRole=2) | `123456789` |

> Password MD5 của `123456789` là: `25f9e794323b453885f5181f1b624db`

---

## Các chức năng của đồ án

### Trang khách hàng (Public)

| STT | Chức năng | Mô tả chi tiết |
|-----|-----------|----------------|
| 1 | **Trang chủ** | Hiển thị banner, phòng xem nhiều nhất, phòng có giảm giá, danh sách dịch vụ |
| 2 | **Xem danh sách phòng** | Phân trang, hiển thị phòng còn trống, thông tin giá, loại phòng |
| 3 | **Chi tiết phòng** | Hình ảnh, mô tả (CKEditor), dịch vụ kèm theo, bình luận & đánh giá sao, phòng liên quan |
| 4 | **Tìm kiếm phòng** | Tìm theo tên phòng, loại phòng, số khách, với phân trang |
| 5 | **Đặt phòng** | Chọn ngày check-in/check-out, dịch vụ đi kèm, tính tổng tiền (đã trừ giảm giá), kiểm tra trùng lịch |
| 6 | **Đăng ký tài khoản** | Form đăng ký, kiểm tra trùng username, gửi OTP qua email |
| 7 | **Xác thực OTP** | Nhập mã OTP 6 số để kích hoạt tài khoản |
| 8 | **Đăng nhập** | Đăng nhập cho khách hàng và nhân viên |
| 9 | **Quên mật khẩu** | Gửi yêu cầu reset mật khẩu qua email |
| 10 | **Lịch sử đặt phòng** | Xem các đơn đã đặt, trạng thái, hủy phòng |
| 11 | **Thanh toán MoMo** | Tích hợp cổng thanh toán MoMo (test) |
| 12 | **Hồ sơ cá nhân** | Xem và cập nhật thông tin, đổi mật khẩu |
| 13 | **Bình luận & đánh giá** | Gửi bình luận kèm sao (1-5 sao) cho từng phòng |
| 14 | **Giới thiệu / Liên hệ / Về chúng tôi** | Các trang nội dung |

### Trang quản trị (Admin)

| STT | Chức năng | Mô tả chi tiết |
|-----|-----------|----------------|
| 1 | **Bảng thống kê (Dashboard)** | Biểu đồ cột doanh thu 12 tháng, tổng quan hệ thống |
| 2 | **Quản lý loại phòng** | Thêm, sửa, xóa loại phòng (chỉ Admin - idRole=1) |
| 3 | **Quản lý phòng** | Thêm, sửa, xóa phòng kèm hình ảnh, mô tả CKEditor, giá, giảm giá, sức chứa |
| 4 | **Quản lý nhân viên** | Thêm, sửa, xóa tài khoản nhân viên (idRole=2) |
| 5 | **Quản lý khách hàng** | Xem, sửa, xóa tài khoản khách hàng (idRole=3) |
| 6 | **Quản lý dịch vụ** | Thêm, sửa, xóa dịch vụ kèm theo phòng |
| 7 | **Quản lý đặt phòng** | Xem danh sách đơn, chi tiết đơn, cập nhật trạng thái & thanh toán |
| 8 | **In hóa đơn** | Xuất hóa đơn/in phiếu thu cho khách |
| 9 | **Đăng nhập/Đăng xuất** | Phân quyền Admin vs Staff |

---

## Map đồ án

### Routing (Định tuyến URL)

| URL | Controller | Action | Mô tả |
|-----|-----------|--------|-------|
| `/` hoặc `/PublicHome/Index` | PublicHome | Index | Trang chủ |
| `/PublicRoom/Index/{page}` | PublicRoom | Index | Danh sách phòng (phân trang) |
| `/PublicRoom/DetailRoom/{id}` | PublicRoom | DetailRoom | Chi tiết phòng |
| `/PublicRoom/Search` | PublicRoom | Search | Tìm kiếm phòng |
| `/PublicAuthentication/Login` | PublicAuthentication | Login | Đăng nhập khách hàng |
| `/PublicAuthentication/Register` | PublicAuthentication | Register | Đăng ký tài khoản |
| `/PublicBooking/GetBookings/{id}` | PublicBooking | GetBookings | Lịch sử đặt phòng |
| `/PublicUser/ProfileUser/{id}` | PublicUser | ProfileUser | Hồ sơ cá nhân |
| `/AdminAuthentication/Login` | AdminAuthentication | Login | Đăng nhập Admin |
| `/AdminHome/Index` | AdminHome | Index | Dashboard |
| `/AdminRoom/Index` | AdminRoom | Index | Quản lý phòng |
| `/AdminType/Index` | AdminType | Index | Quản lý loại phòng |
| `/AdminService/Index` | AdminService | Index | Quản lý dịch vụ |
| `/AdminUser/Index` | AdminUser | Index | Quản lý nhân viên |
| `/AdminUser/Customer` | AdminUser | Customer | Quản lý khách hàng |
| `/AdminBooking/Index` | AdminBooking | Index | Quản lý đặt phòng |
| `/AdminBooking/Bill/{id}` | AdminBooking | Bill | In hóa đơn |

### Database Schema (Sơ đồ bảng)

```
Roles ──────────< Users
 │                   │
 │                   │ (1:N - mỗi User có nhiều Booking)
 │                   ▼
 │              Bookings ──────────< BookingServices
 │               │                          │
 │               ▼                          ▼
 │            Rooms ────────────< RoomComments
 │               │
 │               ▼
             Types

Mô tả quan hệ:
- Roles (1) ──< Users (N): Mỗi vai trò có nhiều người dùng
- Users (1) ──< Bookings (N): Mỗi người dùng có nhiều đơn đặt phòng
- Rooms (1) ──< Bookings (N): Mỗi phòng có nhiều đơn đặt phòng
- Rooms (1) ──< BookingServices (N): (gián tiếp qua Booking)
- BookingServices: liên kết nhiều-nhiều giữa Bookings và Services
- Rooms (1) ──< Types (N): Mỗi loại phòng có nhiều phòng
- Rooms (1) ──< RoomComments (N): Mỗi phòng có nhiều bình luận
- Users (1) ──< RoomComments (N): Mỗi người dùng viết nhiều bình luận
```

### Vai trò người dùng

| idRole | Tên vai trò | Quyền hạn |
|--------|-------------|-----------|
| 1 | Admin (Quản trị viên) | Toàn quyền: quản lý phòng, loại phòng, nhân viên, khách hàng, dịch vụ, đặt phòng |
| 2 | Staff (Nhân viên) | Quản lý dịch vụ, đặt phòng, xem thống kê |
| 3 | Customer (Khách hàng) | Xem phòng, đặt phòng, bình luận, quản lý hồ sơ |

### Trạng thái đặt phòng

| Giá trị | Trạng thái | Mô tả |
|---------|-----------|--------|
| 0 | Chờ xác nhận | Đơn mới, chờ khách sạn xác nhận |
| 1 | Đã nhận phòng | Khách đã check-in |
| 2 | Đã hủy | Khách hủy đơn đặt phòng |
| 3 | Hoàn thành | Khách đã check-out, kết thúc |

---

## Các lỗi thường gặp và cách sửa

### 1. Lỗi "Keyword not supported"

```
ArgumentException: Keyword not supported: '.\sqlexpress01;database'
```

**Nguyên nhân:** Connection string trong `Web.config` sai định dạng.

**Cách sửa:** Mở `Web.config`, sửa phần `<connectionStrings>` cho đúng:

```xml
<connectionStrings>
  <add name="DBConnectionString"
       connectionString="Data Source=.\SQLEXPRESS01;Database=DBQuanLyKhachSan;Integrated Security=True"
       providerName="System.Data.SqlClient" />
</connectionStrings>
```

- `Data Source` → tên server: instance SQL của bạn (`.`, `localhost`, `.\SQLEXPRESS`)
- `Database` → tên database: `DBQuanLyKhachSan`
- Kiểm tra tên server trong SSMS → Object Explorer → Server Name

---

### 2. Lỗi "A network-related or instance-specific error"

```
SqlException: A network-related or instance-specific error occurred while establishing
a connection to SQL Server.
```

**Nguyên nhân:** SQL Server không chạy hoặc tên server không đúng.

**Cách sửa:**
- Mở **SQL Server Configuration Manager** → **SQL Server Services** → Đảm bảo **SQL Server (SQLEXPRESS)** đang chạy (Status: Running).
- Kiểm tra tên server chính xác trong SSMS và cập nhật vào `Web.config`.
- Nếu dùng SQL Server đầy đủ (không phải Express), thử: `Data Source=.` hoặc `Data Source=(local)`.

---

### 3. Lỗi "Cannot attach the file ... as database already exists"

```
SqlException: Cannot attach the file ...\DBQuanLyKhachSan.mdf as 'DBQuanLyKhachSan'
because it already exists.
```

**Nguyên nhân:** Database đã tồn tại trong SQL Server.

**Cách sửa:**
- Mở SSMS → Object Explorer → **Databases** → Click chuột phải vào `DBQuanLyKhachSan` → **Delete** → OK.
- Hoặc dùng lệnh SQL: `DROP DATABASE DBQuanLyKhachSan;` rồi chạy lại script.

---

### 4. Lỗi "Login failed for user" (Windows Authentication)

```
SqlException: Login failed. The login is from an untrusted domain
and cannot be used with Windows authentication.
```

**Nguyên nhân:** Máy tính không join domain hoặc SQL Server không cho phép Windows Authentication.

**Cách sửa:** Đổi sang SQL Server Authentication trong `Web.config`:

```xml
<connectionStrings>
  <add name="DBConnectionString"
       connectionString="Data Source=.\SQLEXPRESS01;Database=DBQuanLyKhachSan;User ID=sa;Password=your_password"
       providerName="System.Data.SqlClient" />
</connectionStrings>
```

Hoặc bật SQL Server Authentication trong SSMS:
- Click phải server → **Properties** → **Security** → Chọn **SQL Server and Windows Authentication mode**.

---

### 5. Lỗi "This project references NuGet package(s) that are missing"

```
Error: This project references NuGet package(s) that are missing on this computer.
```

**Nguyên nhân:** NuGet packages chưa được restore.

**Cách sửa:**
- Trong Visual Studio → Menu **Project** → **Restore NuGet Packages**.
- Hoặc click chuột phải vào Solution → **Restore NuGet Packages**.
- Hoặc chạy lệnh: `nuget restore quanlykhachsan.sln` trong Developer Command Prompt.

---

### 6. Lỗi "The entity type requires a primary key"

**Nguyên nhân:** Entity model thiếu Primary Key hoặc Entity Framework không nhận diện đúng key.

**Cách sửa:** Kiểm tra các Model, đảm bảo mỗi entity có property được decorate `[Key]` hoặc đúng naming convention (`Id`, `idBooking`, `idUser`, ...).

---

### 7. Lỗi "Invalid object name 'dbo.TableName'"

```
SqlException: Invalid object name 'dbo.Bookings'
```

**Nguyên nhân:** Database chưa được tạo hoặc table chưa tồn tại.

**Cách sửa:** Chạy lại file `scriptDML.sql` trong SSMS để tạo đầy đủ database và các bảng.

---

### 8. Lỗi "Could not find a part of the path" (khi upload hình)

```
IOException: Could not find a part of the path 'C:\...\Content\images\...'
```

**Nguyên nhân:** Thư mục `Content/images/` chưa tồn tại hoặc không có quyền ghi.

**Cách sửa:**
- Tạo thư mục `Content/images/` trong `QuanLyKhachSan/`.
- Đảm bảo IIS_IUSRS có quyền ghi vào thư mục.
- Chạy Visual Studio với quyền Administrator.

---

### 9. Lỗi "The 'ObjectContent`1' type failed to serialize the response body"

**Nguyên nhân:** Vấn đề JSON serialization với Entity objects có navigation properties.

**Cách sửa:** Sử dụng `Json(new { ... })` thủ công thay vì trả về entity trực tiếp, hoặc dùng anonymous type:

```csharp
return Json(new { data = list.Select(x => new { x.field1, x.field2 }) });
```

---

### 10. Lỗi trang bị trắng (Blank Page) sau khi copy project sang máy khác

**Nguyên nhân:** Cache trình duyệt hoặc project chưa được build lại.

**Cách sửa:**
- Nhấn `Ctrl + Shift + R` để hard refresh trình duyệt.
- Mở tab ẩn danh / incognito.
- Trong Visual Studio → **Build** → **Clean Solution** → **Rebuild Solution**.
- Xóa thư mục `obj/` và `bin/` rồi build lại.

---

### 11. Lỗi "401 Unauthorized" khi gửi email OTP

**Nguyên nhân:** Email hoặc App Password trong `Web.config` không đúng.

**Cách sửa:**
- Kiểm tra `FormEmailAddress` và `FormEmailPassword` trong `appSettings` trong `Web.config`.
- Đảm bảo đã bật **2-Factor Authentication** trên Gmail và tạo **App Password** (16 ký tự).
- App Password này thay thế cho password thường của Gmail.

---

### 12. Lỗi "Không thấy thay đổi sau khi sửa code"

**Nguyên nhân:** IIS Express đã cache trang.

**Cách sửa:**
- Stop project (nút vuông đỏ trong Visual Studio).
- Trong Solution Explorer → Click chuột phải vào project → **Clean**.
- Xóa thư mục `bin/` và `obj/`.
- Nhấn `Ctrl + F5` (Start Without Debugging) để chạy lại.

---

> **Mẹo chung:** Khi gặp lỗi không rõ nguyên nhân, luôn thử: **Clean Solution** → **Rebuild** → **Run (F5)** trước khi debug sâu.
