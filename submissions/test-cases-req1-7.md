# Test Cases — Bảng trường hợp kiểm thử

| Thông tin      |                       |
| -------------- | --------------------- |
| **Nhóm** | Nhóm STQA - ICT Gen 15 |
| **Ngày tạo** | 23/05/2026            |
| **Hệ thống** | https://stqa.rbc.vn   |
| **Tham chiếu** | SRS v1.0              |

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

### IDM — Đăng nhập (REQ-01)

| Đặc tính (Characteristic)  | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi             |
| -------------------------- | ----------------- | ------------------------ | ---------------------------- |
| Email có tồn tại trong DB? | Có                | `librarian@library.com`  | Chuyển sang trang chủ        |
|                            | Không             | `noone@email.com`        | Từ chối, hiển thị lỗi        |
| Mật khẩu có đúng?          | Đúng              | `admin123`               | Đăng nhập thành công         |
|                            | Sai               | `wrongpass`              | Từ chối, báo lỗi mật khẩu sai|
| Trạng thái ô nhập liệu?    | Đã điền đủ        | (giá trị bất kỳ)         | Xử lý request bình thường    |
|                            | Bỏ trống          | `""`                     | Báo lỗi "Vui lòng nhập..."   |
| Định dạng Email?           | Hợp lệ            | `dam.tran@email.com`     | Xử lý request bình thường    |
|                            | Không hợp lệ      | `abcgmail.com`           | Báo lỗi định dạng email sai  |

### IDM — Quản lý thành viên / Thêm mới (REQ-07)

| Đặc tính (Characteristic)  | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi             |
| -------------------------- | ----------------- | ------------------------ | ---------------------------- |
| Quyền (Role) người dùng?   | Thủ thư           | `librarian@library.com`  | Cho phép thấy nút "Thêm mới" |
|                            | Thành viên thường | `dam.tran@email.com`     | Ẩn nút, chặn truy cập URL    |
| Định dạng Email nhập vào?  | Hợp lệ (có @ và .) | `binh.ly@email.com`      | Cho phép tạo mới             |
|                            | Sai định dạng     | `loi.vu@email`           | Chặn tạo mới, báo lỗi        |
| Tính duy nhất của Email?   | Chưa tồn tại      | `binh.ly@email.com`      | Tạo thành công               |
|                            | Đã tồn tại        | `ba.nguyen@email.com`    | Chặn tạo mới, báo lỗi trùng  |

---

## Bước 2: Test Cases

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi (Strong Oracle) | REQ | Kỹ thuật |
| ----- | ----------------- | -------------- | -------------- | --------------- | ---------------- | --- | -------- |
| **TC-REQ01-01** | Kiểm tra đăng nhập thành công với tài khoản hợp lệ | Trình duyệt đã được làm mới (F5). Đang ở màn hình đăng nhập. | 1. Nhập Email hợp lệ.<br>2. Nhập Mật khẩu hợp lệ.<br>3. Nhấn nút Đăng nhập.<br>4. Quan sát giao diện. | Email: `librarian@library.com`<br>Mật khẩu: `admin123` | Đăng nhập thành công, chuyển sang trang chủ. AppBar hiển thị "Nguyễn Thủ Thư (Thủ thư)". Không có lỗi. | REQ-01 | EP |
| **TC-REQ01-02** | Kiểm tra đăng nhập với mật khẩu sai (Negative Test) | Trình duyệt đã được làm mới (F5). Đang ở màn hình đăng nhập. | 1. Nhập Email hợp lệ.<br>2. Nhập mật khẩu sai.<br>3. Nhấn nút Đăng nhập. | Email: `dam.tran@email.com`<br>Mật khẩu: `wrongpass` | Hệ thống từ chối đăng nhập. Hiển thị thông báo lỗi: “Mật khẩu không đúng”. Không chuyển trang. | REQ-01 | Kịch bản lỗi |
| **TC-REQ01-03** | Kiểm tra đăng nhập với email không tồn tại | Trình duyệt đã được làm mới (F5). Đang ở màn hình đăng nhập. | 1. Nhập Email không tồn tại.<br>2. Nhập mật khẩu bất kỳ.<br>3. Nhấn nút Đăng nhập. | Email: `noone@email.com`<br>Mật khẩu: `password123` | Hệ thống chặn đăng nhập, hiển thị đúng thông báo: “Không tìm thấy thành viên”. Không tạo phiên. | REQ-01 | EP |
| **TC-REQ01-04** | Kiểm tra validate khi bỏ trống Email và Mật khẩu | Trình duyệt đã được làm mới (F5). Đang ở màn hình đăng nhập. | 1. Để trống ô Email.<br>2. Để trống ô Mật khẩu.<br>3. Nhấn nút Đăng nhập. | Email: `""`<br>Mật khẩu: `""` | Hệ thống hiển thị thông báo: “Vui lòng nhập email và mật khẩu”. Không gửi request lên server. | REQ-01 | EP, BVA |
| **TC-REQ01-05** | Kiểm tra định dạng Email không hợp lệ | Trình duyệt đã được làm mới (F5). Đang ở màn hình đăng nhập. | 1. Nhập Email sai định dạng.<br>2. Nhập mật khẩu bất kỳ.<br>3. Nhấn nút Đăng nhập. | Email: `abcgmail.com`<br>Mật khẩu: `password123` | Hệ thống từ chối xử lý. Hiển thị lỗi định dạng Email không hợp lệ trên giao diện. | REQ-01 | EP |
| **TC-REQ07-01** | Thêm thành viên mới thành công | Đăng nhập bằng tài khoản Thủ thư. Đang ở màn hình Thêm thành viên. | 1. Nhập Họ tên.<br>2. Nhập Email hợp lệ chưa tồn tại.<br>3. Nhập SĐT.<br>4. Nhấn nút Thêm mới. | Họ tên: `Lý Tân Binh`<br>Email: `binh.ly@email.com`<br>SĐT: `0988111222` | Hiển thị thông báo "Thêm thành công". Thành viên Lý Tân Binh xuất hiện trong danh sách. | REQ-07 | EP |
| **TC-REQ07-02** | Thêm thất bại do Email sai định dạng | Đăng nhập bằng tài khoản Thủ thư. Đang ở màn hình Thêm thành viên. | 1. Nhập Họ tên.<br>2. Nhập Email thiếu dấu chấm.<br>3. Nhập SĐT.<br>4. Nhấn Thêm mới. | Họ tên: `Vũ Sai Lỗi`<br>Email: `loi.vu@email`<br>SĐT: `0977333444` | Hệ thống không tạo mới. Hiển thị thông báo lỗi "Email không hợp lệ". | REQ-07 | EP |
| **TC-REQ07-03** | Thêm thất bại do Email đã tồn tại trong hệ thống | Đăng nhập bằng tài khoản Thủ thư. Đã có user `ba.nguyen@email.com`. | 1. Nhập Họ tên.<br>2. Nhập Email bị trùng.<br>3. Nhập SĐT.<br>4. Nhấn Thêm mới. | Họ tên: `Người Dùng Trùng`<br>Email: `ba.nguyen@email.com`<br>SĐT: `0999555666` | Hệ thống từ chối lưu. Hiển thị thông báo lỗi "Email đã tồn tại". | REQ-07 | EP |
| **TC-REQ07-04** | Kiểm tra phân quyền: Thành viên không được phép thêm mới | Đăng nhập bằng tài khoản Thành viên thường. | 1. Quan sát màn hình Quản lý thành viên.<br>2. Thử truy cập URL trang Thêm. | Tài khoản: `dam.tran@email.com` | Không hiển thị nút dấu `+`. Nếu cố tình truy cập URL bằng tay, hệ thống đá văng và báo lỗi quyền. | REQ-07 | Bảo mật |

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
| -------------- | ----- | ------- | -------------------- |
| Đăng nhập hệ thống | 5 | REQ-01 | Phân lớp tương đương (EP), Giá trị biên (BVA) |
| Quản lý thành viên | 4 | REQ-07 | Phân lớp tương đương (EP), State-based |
| **Tổng** | **9** | **2 REQs** | |