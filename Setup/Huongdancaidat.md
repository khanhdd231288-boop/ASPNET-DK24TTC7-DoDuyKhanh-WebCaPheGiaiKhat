# HƯỚNG DẪN CÀI ĐẶT WEBSITE BÁN SẢN PHẨM CÀ PHÊ GIẢI KHÁT

## 1. Yêu cầu môi trường

Trước khi chạy project, cần cài đặt các công cụ sau:

- **Visual Studio 2026**
- **.NET SDK** phù hợp với project ASP.NET Core MVC
- **SQL Server**
- **SQL Server Management Studio (SSMS)**

---

## 2. Clone source code

Tải project từ GitHub về máy bằng lệnh:

```bash
git clone <repository-url>
```

Sau đó mở thư mục project.

---

## 3. Mở project trong Visual Studio

- Vào thư mục `src/`
- Mở file solution:

```text
DoDuyKhanh.sln
```

- Chờ Visual Studio restore các package cần thiết

---

## 4. Tạo cơ sở dữ liệu

Có 2 cách để tạo cơ sở dữ liệu:

### Cách 1: Chạy file SQL

Mở **SQL Server Management Studio (SSMS)** và thực hiện:

- Tạo database mới, ví dụ:

```sql
CREATE DATABASE DoDuyKhanhStore;
```

- Chọn database vừa tạo
- Chạy các file SQL trong thư mục `setup/`, ví dụ:
  - `create-database.sql`
  - `sample-data.sql`

### Cách 2: Dùng Entity Framework Core Migration

Nếu project đã có migration, mở **Package Manager Console** và chạy:

```powershell
Update-Database
```

Nếu chưa có database, hệ thống sẽ tự tạo các bảng cần thiết.

---

## 5. Cấu hình chuỗi kết nối

Ở phẩn webconfig

Tìm phần `ConnectionStrings` và chỉnh sửa lại cho phù hợp với máy của bạn:

"ConnectionStrings": {
  "DefaultConnection": "Server=.;Database=DoDuyKhanhStore;Trusted_Connection=True;TrustServerCertificate=True"
}
```

Trong đó:

- `Server=.` : dùng SQL Server trên máy cục bộ
- `Database=DoDuyKhanhStore` : tên cơ sở dữ liệu
- `Trusted_Connection=True` : đăng nhập bằng tài khoản Windows
- `TrustServerCertificate=True` : bỏ qua cảnh báo chứng chỉ trong môi trường local

Nếu dùng SQL Server Authentication thì có thể sửa thành:

```json
"ConnectionStrings": {
  "DefaultConnection": "Server=.;Database=DoDuyKhanhStore;User Id=sa;Password=your_password;TrustServerCertificate=True"
}
```

---

## 6. Chạy chương trình

Sau khi cấu hình xong:

- Nhấn **Ctrl + F5** hoặc **F5** trong Visual Studio
- Hệ thống sẽ chạy trên trình duyệt với địa chỉ localhost, ví dụ:

```text
https://localhost:xxxx
```

---

Truy cập bằng tài khoản admin

https://localhost:xxxx/admin

- **TK:** admin
- **Mật khẩu:** 123456

---

## 8. Cấu trúc thư mục liên quan

```text
setup/
├── Huongdancaidat.md
├── database.sql
```

- `Huongdancaidat.md`: tài liệu hướng dẫn cài đặt
- `database.sql`: file tạo bảng dữ liệu

---

## 9. Một số lỗi thường gặp

### Không kết nối được database

- Kiểm tra lại tên database 
- Kiểm tra SQL Server đã chạy chưa
- Kiểm tra đúng tên server chưa

### Lỗi thiếu bảng dữ liệu

- Chạy lại file SQL tạo bảng
- Hoặc chạy lại lệnh:

```powershell
Update-Database
```

### Không đăng nhập được admin

- Kiểm tra tài khoản admin đã được thêm vào bảng `Customers` chưa
- Kiểm tra cột `Role` đã có giá trị `Admin` chưa

---

## 10. Kết luận

Sau khi thực hiện đầy đủ các bước trên, hệ thống website bán sản phẩm cà phê giải khát có thể chạy được trên máy cục bộ, hỗ trợ các chức năng cơ bản dành cho người dùng và quản trị viên.
