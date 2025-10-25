# 🎭 Sơ đồ Use Case - Hệ thống Quản lý Chấm Công / Giao dịch nội bộ

## 🎯 Mục tiêu
Sơ đồ Use Case mô tả **các chức năng chính mà người dùng có thể tương tác với hệ thống**.  
Mỗi use case thể hiện một **nghiệp vụ cụ thể** mà hệ thống cung cấp cho từng loại người dùng (actor).

---

## 🧩 Các tác nhân (Actors)

| Tác nhân | Mô tả vai trò |
|-----------|---------------|
| **Nhân viên (Employee)** | Người sử dụng chính của hệ thống, thực hiện chấm công, xem lịch sử, và gửi yêu cầu chỉnh sửa. |
| **Quản lý (Manager)** | Người giám sát chấm công, phê duyệt hoặc từ chối yêu cầu chỉnh sửa, và xuất báo cáo. |
| **Hệ thống (System)** | Thực hiện tự động xử lý nghiệp vụ: lưu trữ, kiểm tra logic, đồng bộ dữ liệu. |
| **Quản trị viên (Admin)** | Người quản lý cấp cao, chịu trách nhiệm quản lý tài khoản và phân quyền người dùng. |

---

## ⚙️ Các Use Case chính

| Tên Use Case | Actor chính | Mô tả ngắn |
|---------------|-------------|-------------|
| **Đăng nhập hệ thống** | Nhân viên, Quản lý, Admin | Cho phép người dùng đăng nhập bằng tài khoản hợp lệ. |
| **Chấm công (Check-in/Check-out)** | Nhân viên | Ghi nhận thời gian vào – ra của nhân viên trong ca làm việc. |
| **Xem lịch sử chấm công** | Nhân viên | Hiển thị các bản ghi chấm công trước đó. |
| **Gửi yêu cầu chỉnh sửa / khiếu nại** | Nhân viên | Gửi yêu cầu sửa dữ liệu khi có sai sót (ví dụ quên check-out). |
| **Phê duyệt yêu cầu chỉnh sửa** | Quản lý | Xem và xác nhận hoặc từ chối các yêu cầu chỉnh sửa. |
| **Quản lý thông tin nhân viên** | Quản lý, Admin | Cập nhật thông tin, thêm hoặc ngưng hoạt động nhân viên. |
| **Xuất báo cáo chấm công** | Quản lý | Xuất dữ liệu chấm công ra file (PDF/Excel) để theo dõi. |
| **Quản lý tài khoản người dùng** | Admin | Tạo, phân quyền và vô hiệu hóa tài khoản. |
| **Đồng bộ dữ liệu hệ thống** | System | Thực hiện tự động lưu và cập nhật dữ liệu định kỳ. |

---

## 🔁 Quan hệ giữa các Use Case

| Loại quan hệ | Mô tả |
|---------------|--------|
| **«include»** | Một Use Case phụ được gọi bắt buộc trong quá trình thực hiện Use Case chính. |
| **«extend»** | Một Use Case mở rộng, chỉ thực hiện trong điều kiện đặc biệt. |

### Ví dụ quan hệ:
- `Đăng nhập` **«include»** `Xác thực tài khoản`
- `Gửi yêu cầu chỉnh sửa` **«extend»** `Xem lịch sử chấm công`
- `Phê duyệt yêu cầu chỉnh sửa` **«include»** `Kiểm tra dữ liệu chấm công`
- `Xuất báo cáo` **«include»** `Tổng hợp dữ liệu`

---

## 🧭 Mô tả tổng quát bằng văn bản UML

Actor: Nhân viên
- Đăng nhập hệ thống
- Chấm công
- Xem lịch sử chấm công
- Gửi yêu cầu chỉnh sửa (extends Xem lịch sử chấm công)

Actor: Quản lý
- Đăng nhập hệ thống
- Phê duyệt yêu cầu chỉnh sửa (includes Kiểm tra dữ liệu chấm công)
- Xuất báo cáo chấm công (includes Tổng hợp dữ liệu)
- Quản lý thông tin nhân viên

Actor: Admin
- Đăng nhập hệ thống
- Quản lý tài khoản người dùng
- Quản lý thông tin nhân viên

Actor: Hệ thống
- Đồng bộ dữ liệu hệ thống
- Lưu trữ và xử lý logic tự động

---

## 🧱 Cấu trúc sơ đồ gợi ý

- **Hình elip (oval):** biểu diễn mỗi Use Case  
- **Hình người:** biểu diễn các Actor  
- **Đường thẳng nối:** quan hệ giữa Actor ↔ Use Case  
- **«include» / «extend»:** thể hiện mối quan hệ chức năng giữa các Use Case  
- **Hệ thống (System Boundary):** khung bao toàn bộ các Use Case

---

## 📘 Ghi chú triển khai
- Sơ đồ Use Case này là **tổng quát**, dùng để mô tả toàn bộ chức năng chính của hệ thống.
- Có thể chia thành các sơ đồ con:
  - Use Case **nhân viên**
  - Use Case **quản lý**
  - Use Case **admin**
- Phù hợp cho giai đoạn **phân tích nghiệp vụ (Analysis)** trong mô hình **UML/SDLC**.
