# Danh sách Báo cáo lỗi (Bug Reports) - Phân hệ Quản lý thành viên (REQ-07)

---

## 1. BUG-01: Chặn nhầm email hợp lệ

**Bug ID:** BUG-01 (Tham chiếu: TC-REQ07-01)

**Tiêu đề:** Hệ thống báo lỗi "Email không hợp lệ" và từ chối thêm mới khi nhập email hoàn toàn đúng định dạng (VD: binh.ly@email.com)

**Môi trường:**
- Trình duyệt: Chrome Version 125.0.0
- Hệ điều hành: Windows / macOS
- Ứng dụng: Hệ thống Mượn sách thư viện (https://stqa.rbc.vn)

**Điều kiện tiên quyết:**
- Người dùng đã đăng nhập thành công bằng tài khoản **Thủ thư** (`librarian@library.com`).
- Đang truy cập ở màn hình **Thêm thành viên mới**.

**Bước tái hiện:**
1. Tại ô **Họ và tên**, nhập: `Lý Tân Binh`.
2. Tại ô **Email**, nhập email hợp lệ có chứa dấu chấm trước @: `binh.ly@email.com`.
3. Tại ô **Số điện thoại**, nhập: `0988111222`.
4. Nhấn nút **Thêm thành viên** màu xanh ở dưới cùng.

**Kết quả mong đợi:**
Hệ thống chấp nhận dữ liệu (do email đã thỏa mãn quy tắc có `@` và có dấu `.` trong domain theo SRS), tiến hành thêm mới thành viên và hiển thị thông báo thêm thành công.

**Kết quả thực tế:**
Hệ thống không lưu dữ liệu, xuất hiện khung cảnh báo màu đỏ với dòng chữ `"Email không hợp lệ."` ngay phía trên nút Thêm thành viên.

**Tác động:**
Nghiệp vụ thêm mới thành viên bị chặn một cách sai lệch đối với những người dùng có địa chỉ email hợp lệ phổ biến (định dạng `[tên].[họ]@domain.com`). Gây bức xúc và gián đoạn công việc của Thủ thư.

**Mức độ:**
**Cao (High)** — Lỗi logic (Validation Logic) làm hỏng luồng chức năng chính của việc Quản lý thành viên. Ngăn cản trực tiếp việc nhập liệu hợp lệ vào hệ thống.

**Minh chứng:**
- Ảnh chụp màn hình đính kèm: `docs/assets/bug01-email-hop-le-bi-loi.png` *(Hiển thị form nhập liệu và thông báo lỗi đỏ)*.

**Đề xuất xử lý:**
Kiểm tra lại hàm kiểm tra định dạng email (Regex Validation) ở mã nguồn Frontend và Backend. Cần cập nhật Regex để cho phép ký tự dấu chấm (`.`) nằm ở phần Tên người dùng (Local part - trước dấu `@`).

---

## 2. BUG-02: Bỏ lọt email sai định dạng

**Bug ID:** BUG-02 (Tham chiếu: TC-REQ07-02)

**Tiêu đề:** Hệ thống cho phép thêm thành viên thành công khi nhập email sai định dạng (thiếu dấu chấm trong phần domain)

**Môi trường:**
- Trình duyệt: Chrome Version 125.0.0
- Hệ điều hành: Windows / macOS
- Ứng dụng: Hệ thống Mượn sách thư viện (https://stqa.rbc.vn)

**Điều kiện tiên quyết:**
- Người dùng đã đăng nhập thành công bằng tài khoản **Thủ thư** (`librarian@library.com`).
- Đang truy cập ở màn hình **Thêm thành viên mới**.

**Bước tái hiện:**
1. Tại ô **Họ và tên**, nhập: `Vũ Sai Lỗi`.
2. Tại ô **Email**, nhập email thiếu dấu chấm (`.`) sau ký tự `@`: `loi.vu@email`.
3. Tại ô **Số điện thoại**, nhập: `0977333444`.
4. Nhấn nút **Thêm thành viên**.

**Kết quả mong đợi:**
Hệ thống từ chối tạo mới dữ liệu, hiển thị thông báo lỗi yêu cầu kiểm tra lại định dạng email (Do SRS quy định rõ: *"Email phải có dấu . trong phần domain"*).

**Kết quả thực tế:**
Hệ thống không phát hiện ra lỗi, vẫn chấp nhận lưu dữ liệu và hiển thị thông báo thêm thành viên thành công. 

**Tác động:**
Dữ liệu rác, sai định dạng được đưa vào hệ thống cơ sở dữ liệu. Vi phạm quy tắc ràng buộc dữ liệu cơ bản, có thể gây lỗi cho các hệ thống gửi email tự động sau này.

**Mức độ:**
**Cao (High)** — Lỗ hổng trong việc Validate dữ liệu đầu vào, ảnh hưởng trực tiếp đến tính toàn vẹn và chính xác của dữ liệu (Data Integrity).

**Minh chứng:**
- Ảnh chụp màn hình đính kèm: `docs/assets/bug02-chap-nhan-email-sai.png` *(Hiển thị thông báo thêm thành công với email sai)*.

**Đề xuất xử lý:**
Bổ sung hoặc cập nhật lại biểu thức chính quy (Regex Validation) kiểm tra email. Bắt buộc phải có điều kiện kiểm tra sự tồn tại của ít nhất một dấu chấm (`.`) nằm ở phía sau ký tự `@` (Ví dụ: `@domain.com`).