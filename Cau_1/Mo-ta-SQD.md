# 📘 Sequence Diagram – Hệ thống Quản lý Chấm Công

## 🧩 1. Giới thiệu
Tài liệu này mô tả **Sơ đồ tuần tự (Sequence Diagram)** tổng quát của hệ thống **Quản lý chấm công**.  
Sơ đồ biểu diễn chuỗi tương tác giữa các **tác nhân (Actors)** và **đối tượng trong hệ thống (Objects)** qua các tiến trình chính:  
- Đăng nhập  
- Chấm công (Check-in / Check-out)  
- Gửi yêu cầu chỉnh sửa / khiếu nại  
- Quản lý phê duyệt  
- Xuất báo cáo chấm công  

---

## 🧠 2. Mục đích của sơ đồ
Sequence Diagram được sử dụng để:
- Mô tả **luồng tương tác động** giữa các thành phần của hệ thống.  
- Làm rõ **thứ tự các thông điệp** được gửi đi trong mỗi tiến trình nghiệp vụ.  
- Hỗ trợ thiết kế logic hệ thống từ **Use Case Diagram** và **Class Diagram** trước đó.  

---

## 🧍‍♂️ 3. Các tác nhân (Actors)
| Tác nhân | Vai trò | Mô tả hành động |
|-----------|----------|----------------|
| **User** | Người dùng tổng quát | Thực hiện đăng nhập hệ thống |
| **Nhân viên** | Người chấm công | Thực hiện Check-in / Check-out và gửi yêu cầu chỉnh sửa |
| **Quản lý** | Người duyệt | Phê duyệt, phản hồi yêu cầu, xuất báo cáo |
| **Admin** | Quản trị hệ thống | Giám sát, bảo trì, kiểm tra dữ liệu |
| **CSDL** | Lưu trữ dữ liệu | Lưu toàn bộ thông tin người dùng, chấm công, và báo cáo |

---

## 🔄 4. Luồng trình tự tổng quát

### 4.1. Đăng nhập hệ thống
1. **User** gửi yêu cầu `Đăng nhập(username, password)` tới hệ thống.  
2. **Hệ thống** truy vấn **CSDL** để xác thực.  
3. **CSDL** trả kết quả xác thực.  
4. **Hệ thống** phản hồi kết quả đăng nhập cho **User**.

---

### 4.2. Thực hiện Check-in / Check-out
1. **Nhân viên** gửi yêu cầu `Check-in()` đến hệ thống chấm công.  
2. **Hệ thống** ghi nhận dữ liệu: *ngày công, thời gian, vị trí*.  
3. Cuối ca làm việc, **Nhân viên** gửi yêu cầu `Check-out()`.  
4. **Hệ thống** cập nhật và lưu dữ liệu công vào **Báo cáo chấm công**.

---

### 4.3. Gửi yêu cầu chỉnh sửa / khiếu nại
1. **Nhân viên** gửi `Yêu cầu chỉnh sửa` với thông tin cần thay đổi.  
2. **Hệ thống yêu cầu chỉnh sửa** ghi nhận và chuyển đến **Quản lý**.  
3. **Quản lý** xem xét → thực hiện `Phê duyệt` hoặc `Từ chối`.  
4. **Hệ thống** gửi phản hồi kết quả lại cho **Nhân viên**.

---

### 4.4. Phê duyệt và phản hồi
1. **Quản lý** truy cập danh sách yêu cầu đang chờ.  
2. **Hệ thống** lấy dữ liệu từ **CSDL** và hiển thị thông tin chi tiết.  
3. **Quản lý** chọn hành động `Chấp thuận`, `Từ chối` hoặc `Yêu cầu bổ sung`.  
4. **Hệ thống** cập nhật trạng thái và thông báo đến **Nhân viên**.

---

### 4.5. Xuất báo cáo chấm công
1. **Quản lý** gửi yêu cầu `Xuất báo cáo` theo ngày/tháng/phòng ban.  
2. **Hệ thống báo cáo** tổng hợp dữ liệu từ các bản ghi chấm công và yêu cầu chỉnh sửa.  
3. **Báo cáo** được tạo (PDF/Excel) và trả về cho **Quản lý**.  
4. **Admin** có thể giám sát, lưu trữ và kiểm tra nhật ký báo cáo.

---

## 🧩 5. Các đối tượng trong sơ đồ tuần tự
| Đối tượng | Mô tả |
|------------|--------|
| **Hệ thống chấm công** | Quản lý toàn bộ quá trình Check-in/Check-out |
| **Hệ thống yêu cầu chỉnh sửa** | Tiếp nhận và xử lý yêu cầu của nhân viên |
| **Báo cáo chấm công** | Tổng hợp dữ liệu và xuất báo cáo thống kê |
| **CSDL (Database)** | Lưu trữ tất cả thông tin nghiệp vụ và người dùng |

---

## 🧮 6. Biểu đồ PlantUML minh họa

```plantuml
@startuml
actor User
actor "Nhân viên" as Employee
actor "Quản lý" as Manager
participant "Hệ thống chấm công" as System
participant "Yêu cầu chỉnh sửa" as Request
participant "Báo cáo chấm công" as Report
database "CSDL" as DB

User -> System: Đăng nhập()
System -> DB: Kiểm tra thông tin đăng nhập
DB --> System: Thông tin hợp lệ
System --> User: Đăng nhập thành công

Employee -> System: Check-in()
System -> DB: Ghi thời gian vào
Employee -> System: Check-out()
System -> DB: Cập nhật thời gian ra

Employee -> Request: Gửi yêu cầu chỉnh sửa()
Request -> Manager: Chuyển yêu cầu
Manager -> Request: Duyệt hoặc từ chối
Request -> Employee: Thông báo kết quả

Manager -> Report: Xuất báo cáo()
Report -> DB: Truy xuất dữ liệu chấm công
Report --> Manager: Trả về báo cáo
@enduml
