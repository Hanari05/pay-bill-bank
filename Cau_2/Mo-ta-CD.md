# 🧩 Class Diagram - Hệ thống Quản lý Chấm Công

## 🎯 Mục tiêu
Sơ đồ **Class Diagram (Sơ đồ lớp)** mô tả **cấu trúc hướng đối tượng** của hệ thống quản lý chấm công.  
Nó cho biết các **lớp chính (classes)**, **thuộc tính (attributes)**, **phương thức (operations)**, và **mối quan hệ (relationships)** giữa các đối tượng trong hệ thống.

---

## 🧱 1. Tổng quan kiến trúc

Hệ thống bao gồm 3 nhóm lớp chính:

| Nhóm | Các lớp tiêu biểu | Vai trò |
|------|-------------------|----------|
| **Người dùng (User Layer)** | `User`, `Nhân viên`, `Quản lý`, `Admin` | Đại diện cho các loại người dùng khác nhau trong hệ thống |
| **Nghiệp vụ chấm công (Business Layer)** | `Checkin/Checkout`, `Yêu cầu chỉnh sửa`, `Báo cáo chấm công`, `Quản lý ca làm` | Xử lý các nghiệp vụ chấm công và báo cáo |
| **Quản trị hệ thống (System Layer)** | `Quản lý nhân viên` | Hỗ trợ quản trị dữ liệu và điều hành nhân sự |

---

## 👤 2. Lớp cơ sở `User`

**Thuộc tính**
- `ID User : int`
- `Tên người dùng : String`
- `Mật khẩu : String`
- `Email : String`
- `Vai trò : String`

**Phương thức**
- `+ Đăng nhập()`
- `+ Đăng xuất()`

**Mô tả:**  
Lớp `User` là **lớp cha** (superclass) cung cấp các thuộc tính và chức năng chung cho tất cả các loại người dùng trong hệ thống.

---

## 👩‍💼 3. Lớp `Nhân viên`

**Thuộc tính**
- `ID nhân viên : int`
- `Tên : String`
- `Chức vụ : String`
- `Vị trí phòng ban : String`

**Phương thức**
- `+ Checkin / Checkout()`
- `+ Xem lịch sử chấm công()`
- `+ Yêu cầu / Khiếu nại()`

**Mối quan hệ**
- Kế thừa từ `User`
- 1 nhân viên có thể có nhiều bản ghi `Checkin/Checkout`
- 1 nhân viên có thể gửi nhiều `Yêu cầu chỉnh sửa`

**Mô tả:**  
Đại diện cho người dùng thông thường – nhân viên.  
Họ có thể chấm công, xem lịch sử làm việc, và gửi yêu cầu khiếu nại nếu phát hiện sai sót.

---

## 🧑‍💼 4. Lớp `Quản lý`

**Phương thức**
- `+ Quản lý nhân viên()`
- `+ Quản lý ca làm việc()`
- `+ Thống kê, báo cáo giờ công()`
- `+ Phản hồi yêu cầu / Khiếu nại()`

**Mối quan hệ**
- Kế thừa từ `User`
- 1 quản lý quản lý nhiều nhân viên (1..*)
- 1 quản lý có nhiều `Báo cáo chấm công`
- 1 quản lý có thể duyệt hoặc từ chối nhiều `Yêu cầu chỉnh sửa`

**Mô tả:**  
Người giám sát trực tiếp nhân viên, chịu trách nhiệm thống kê, báo cáo và phê duyệt yêu cầu chỉnh sửa chấm công.

---

## 🧑‍💻 5. Lớp `Admin`

**Phương thức**
- `+ Bảo mật và kiểm soát truy cập()`
- `+ Giám sát và vận hành()`
- `+ Cải tiến và bảo trì()`
- `+ Quản lý hệ thống()`
- `+ Quản lý dữ liệu và báo cáo cấp cao()`

**Mối quan hệ**
- Kế thừa từ `User`

**Mô tả:**  
Người quản trị hệ thống, chịu trách nhiệm bảo mật, vận hành và bảo trì phần mềm, đồng thời quản lý dữ liệu ở cấp cao.

---

## 🕒 6. Lớp `Checkin / Checkout`

**Thuộc tính**
- `QR chấm công : String`
- `Ngày chấm công : Date`
- `Thời gian chấm công : Time`
- `Trạng thái nhân viên chấm công : String`

**Phương thức**
- `+ Ghi lại báo cáo chấm công()`

**Mối quan hệ**
- 1 nhân viên có thể có nhiều bản ghi `Checkin / Checkout`
- Mỗi bản ghi có thể liên kết với 0..* `Yêu cầu chỉnh sửa chấm công`

**Mô tả:**  
Ghi lại hoạt động check-in/check-out hằng ngày của nhân viên.

---

## 🧾 7. Lớp `Yêu cầu chỉnh sửa chấm công`

**Thuộc tính**
- `ID nhân viên : int`
- `Xác nhận yêu cầu : boolean`
- `ID chấm công : int`
- `Ngày nộp : String`
- `Nguyên nhân : String`
- `Trạng thái cập nhật : String`

**Phương thức**
- `+ Đệ trình yêu cầu()`
- `+ Phê duyệt / Từ chối yêu cầu()`

**Mối quan hệ**
- Mỗi yêu cầu thuộc về 1 nhân viên
- 1 quản lý có thể duyệt nhiều yêu cầu

**Mô tả:**  
Đại diện cho quy trình khi nhân viên gửi yêu cầu sửa dữ liệu chấm công sai hoặc thiếu.

---

## 📊 8. Lớp `Báo cáo chấm công`

**Thuộc tính**
- `ID báo cáo : int`
- `Format và dữ liệu : String`
- `Nội dung báo cáo : String`

**Phương thức**
- `+ Kết quả báo cáo()`
- `+ Xuất file()`

**Mối quan hệ**
- 1 quản lý có thể tạo nhiều báo cáo
- Báo cáo có thể tổng hợp nhiều ca làm việc

**Mô tả:**  
Tổng hợp thông tin chấm công và xuất báo cáo theo kỳ (tuần/tháng).

---

## 📅 9. Lớp `Quản lý ca làm`

**Thuộc tính**
- `Thông tin ca làm việc : String`
- `Ngày : Date`
- `Giờ bắt đầu : Time`
- `Giờ kết thúc : Time`

**Phương thức**
- `+ Đăng ký ca làm việc()`
- `+ Cập nhật ca làm việc()`

**Mối quan hệ**
- Mỗi quản lý có thể quản lý nhiều ca làm (1..*)
- Mỗi ca làm có thể liên kết với nhiều nhân viên (0..*)

**Mô tả:**  
Dùng để tổ chức lịch làm việc cho nhân viên và thống kê khung giờ làm.

---

## 👥 10. Lớp `Quản lý nhân viên`

**Thuộc tính**
- `Thông tin nhân viên : String`
- `Thông tin ca làm : String`

**Phương thức**
- `+ Thêm thông tin nhân viên()`
- `+ Xóa thông tin nhân viên()`
- `+ Sửa thông tin nhân viên()`

**Mối quan hệ**
- Kết hợp với lớp `Quản lý`

**Mô tả:**  
Cung cấp chức năng CRUD (Create, Read, Update, Delete) cho dữ liệu nhân viên.

---

## 🔗 11. Mối quan hệ giữa các lớp

| Loại quan hệ | Mô tả |
|---------------|--------|
| **Kế thừa (Inheritance)** | `Nhân viên`, `Quản lý`, `Admin` kế thừa từ `User` |
| **Kết hợp (Association)** | `Quản lý` ↔ `Báo cáo chấm công`, `Nhân viên` ↔ `Checkin/Checkout` |
| **Tập hợp (Aggregation)** | `Quản lý` tập hợp nhiều `Yêu cầu chỉnh sửa` và `Báo cáo` |
| **Thành phần (Composition)** | `Checkin/Checkout` chứa các bản ghi gắn liền với nhân viên |

---

## 📘 12. Nhận xét tổng quát

- Thiết kế **chuẩn UML** và bám sát nghiệp vụ thực tế.  
- Áp dụng **kế thừa hợp lý** từ lớp `User` để giảm trùng lặp.  
- Các **mối quan hệ nhiều – một (1..*)** được thể hiện chính xác.  
- Có thể chia module rõ ràng:
  - **Module Nhân viên:** Checkin, Khiếu nại
  - **Module Quản lý:** Báo cáo, Phê duyệt
  - **Module Admin:** Quản trị và bảo mật
- Dễ dàng chuyển đổi sang mô hình **ERD hoặc thiết kế CSDL** trong MySQL.

