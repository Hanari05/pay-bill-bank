# 🕒 Sơ đồ trạng thái (State Diagram) - Hệ thống quản lý chấm công

## 🎯 Mục tiêu
Sơ đồ trạng thái này mô tả **vòng đời của một bản ghi chấm công (Attendance Record)** trong hệ thống quản lý chấm công.  
Nó thể hiện các **trạng thái khác nhau** mà bản ghi chấm công có thể trải qua — từ khi nhân viên **Check-in** đến khi bản ghi **được xác nhận, chỉnh sửa hoặc lưu trữ**.

---

## 🧩 Đối tượng được mô tả
**Đối tượng:** `Bản ghi chấm công`  
Đây là thông tin được tạo khi nhân viên thực hiện chấm công trong hệ thống (Check-in/Check-out).

---

## ⚙️ Các trạng thái chính

| Trạng thái | Mô tả |
|-------------|-------|
| **Khởi tạo (Initialized)** | Hệ thống tạo bản ghi khi nhân viên bắt đầu ca làm việc (Check-in). |
| **Đang làm việc (In Progress)** | Bản ghi ghi nhận trạng thái đang trong ca làm việc. |
| **Hoàn thành (Completed)** | Nhân viên Check-out, ca làm việc kết thúc. |
| **Chờ xác nhận (Pending Approval)** | Dữ liệu chấm công được gửi lên chờ quản lý kiểm tra, xác nhận. |
| **Đã xác nhận (Approved)** | Bản ghi được quản lý duyệt hợp lệ. |
| **Bị khiếu nại (Disputed)** | Nhân viên gửi khiếu nại hoặc yêu cầu chỉnh sửa bản ghi. |
| **Đang xử lý khiếu nại (Under Review)** | Quản lý đang xem xét yêu cầu khiếu nại. |
| **Đã chỉnh sửa (Adjusted)** | Khiếu nại được chấp thuận và bản ghi đã được chỉnh sửa. |
| **Từ chối khiếu nại (Rejected)** | Quản lý bác bỏ yêu cầu khiếu nại. |
| **Lưu trữ (Archived)** | Bản ghi được lưu vào kho dữ liệu sau khi hoàn tất quy trình. |

---

## 🔁 Các sự kiện / hành động chuyển trạng thái

| Sự kiện | Chuyển từ → sang | Diễn giải |
|----------|------------------|-----------|
| **Check-in** | Khởi tạo → Đang làm việc | Nhân viên bắt đầu ca làm việc. |
| **Check-out** | Đang làm việc → Hoàn thành | Nhân viên kết thúc ca làm việc. |
| **Gửi dữ liệu** | Hoàn thành → Chờ xác nhận | Hệ thống chuyển dữ liệu chấm công lên để duyệt. |
| **Duyệt hợp lệ** | Chờ xác nhận → Đã xác nhận | Quản lý kiểm tra và duyệt dữ liệu. |
| **Gửi khiếu nại** | Đã xác nhận → Bị khiếu nại | Nhân viên phát hiện sai sót và khiếu nại. |
| **Quản lý xem xét** | Bị khiếu nại → Đang xử lý khiếu nại | Quản lý bắt đầu xử lý yêu cầu. |
| **Chấp thuận** | Đang xử lý khiếu nại → Đã chỉnh sửa | Khiếu nại hợp lệ, hệ thống cập nhật bản ghi. |
| **Bác bỏ** | Đang xử lý khiếu nại → Từ chối khiếu nại | Khiếu nại không hợp lệ. |
| **Hoàn tất xử lý** | Đã chỉnh sửa / Từ chối khiếu nại → Lưu trữ | Kết thúc quá trình xử lý khiếu nại. |
| **Kết thúc chu kỳ** | Đã xác nhận → Lưu trữ | Chu kỳ chấm công hoàn tất. |

---

## 🧭 Mô tả tổng quát bằng văn bản UML
⚫ → Khởi tạo
Khởi tạo → Đang làm việc : Check-in
Đang làm việc → Hoàn thành : Check-out
Hoàn thành → Chờ xác nhận : Gửi dữ liệu
Chờ xác nhận → Đã xác nhận : Duyệt hợp lệ
Đã xác nhận → Bị khiếu nại : Gửi khiếu nại
Bị khiếu nại → Đang xử lý khiếu nại : Quản lý xem xét
Đang xử lý khiếu nại → Đã chỉnh sửa : Chấp thuận
Đang xử lý khiếu nại → Từ chối khiếu nại : Bác bỏ
Đã chỉnh sửa → Lưu trữ : Hoàn tất xử lý
Từ chối khiếu nại → Lưu trữ : Hoàn tất xử lý
Đã xác nhận → Lưu trữ : Kết thúc chu kỳ
Lưu trữ → ⭕

---

## 🧱 Gợi ý trình bày sơ đồ

- **Biểu tượng:**
  - ⚫ Trạng thái bắt đầu  
  - ⭕ Trạng thái kết thúc  
  - ⬜ Hình chữ nhật bo góc: trạng thái trung gian  
  - → Mũi tên có nhãn: mô tả hành động gây ra sự chuyển đổi

- **Nhóm màu gợi ý:**
  - Màu xanh dương nhạt → Trạng thái của nhân viên  
  - Màu cam → Trạng thái xác nhận  
  - Màu vàng → Trạng thái khiếu nại / xử lý  
  - Màu xám → Trạng thái hệ thống (Lưu trữ)

---

## 📘 Ghi chú
- Sơ đồ này là **mô hình tổng quát**, có thể mở rộng thêm các nhánh phụ như:
  - “Hoàn thành → Lưu trữ” (khi hệ thống tự động xác nhận)
  - “Chờ xác nhận → Bị khiếu nại” (trường hợp khiếu nại trước khi duyệt)
- Được dùng để **thiết kế logic nghiệp vụ hoặc mô phỏng vòng đời dữ liệu** trong giai đoạn phân tích hệ thống.

