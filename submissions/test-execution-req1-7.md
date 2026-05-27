# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin         |                                    |
| ----------------- | ---------------------------------- |
| **Nhóm** | Nhóm STQA - ICT Gen 15             |
| **Ngày thực thi** | 23/05/2026                         |
| **Trình duyệt** | Chrome Version 125.0.0             |
| **Hệ điều hành** | Windows / macOS                    |

---

## Kết quả chi tiết

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
| ----- | -------------- | -------------------------- | --------------- | -------- | ---------- | --- |
| **TC-REQ01-01** | REQ-01: Đăng nhập | Đăng nhập thành công với email và mật khẩu hợp lệ, chuyển sang trang chủ. | Hệ thống đăng nhập thành công, chuyển sang trang chủ. AppBar hiển thị đúng tên và vai trò. | **Pass** | <img src="image-1.png" width="150"> | Không có |
| **TC-REQ01-02** | REQ-01: Đăng nhập | Từ chối đăng nhập với mật khẩu sai, báo lỗi "Mật khẩu không đúng". | Hệ thống từ chối đăng nhập, hiển thị đúng thông báo lỗi mật khẩu. | **Pass** | <img src="image-2.png" width="150"> | Không có |
| **TC-REQ01-03** | REQ-01: Đăng nhập | Từ chối đăng nhập với email không tồn tại, báo lỗi "Không tìm thấy thành viên". | Hệ thống từ chối đăng nhập, hiển thị chính xác thông báo lỗi tài khoản không tồn tại. | **Pass** | <img src="image-3.png" width="150"> | Không có |
| **TC-REQ01-04** | REQ-01: Đăng nhập | Báo lỗi "Vui lòng nhập email và mật khẩu" khi bỏ trống trường nhập liệu. | Hiển thị đúng thông báo yêu cầu nhập liệu, không gửi request lên máy chủ. | **Pass** | <img src="image-4.png" width="150"> | Không có |
| **TC-REQ01-05** | REQ-01: Đăng nhập | Từ chối xử lý khi email sai định dạng (thiếu @ hoặc dấu .). | Giao diện chặn đăng nhập, báo lỗi định dạng email không hợp lệ. | **Pass** | <img src="image-5.png" width="150"> | Không có |
| **TC-REQ07-01** | REQ-07: Quản lý thành viên | Thủ thư thêm thành viên mới thành công với email hợp lệ (binh.ly@email.com). | Hệ thống từ chối thêm mới và báo lỗi đỏ "Email không hợp lệ" dù email hoàn toàn đúng định dạng. | **Fail** | <img src="image-6.png" width="150"> | BUG-01 |
| **TC-REQ07-02** | REQ-07: Quản lý thành viên | Chặn thêm mới và báo lỗi khi nhập email sai định dạng (loi.vu@email). | Hệ thống không bắt lỗi định dạng, vẫn chấp nhận và thông báo thêm thành viên thành công. | **Fail** | <img src="image-7.png" width="150"> | BUG-02 |
| **TC-REQ07-03** | REQ-07: Quản lý thành viên | Chặn thêm mới khi nhập email đã tồn tại (ba.nguyen@email.com). | Hệ thống từ chối tạo mới, hiển thị đúng thông báo "Email đã tồn tại". | **Pass** | <img src="image-8.png" width="150"> | Không có |
| **TC-REQ07-04** | REQ-07: Quản lý thành viên | Tài khoản thường không có nút Thêm mới, cố tình truy cập URL sẽ bị chặn. | Nút Thêm mới bị ẩn. Khi cố tình dán URL để truy cập, hệ thống tự động đẩy về màn hình chính, không cho phép truy cập. | **Pass** | <img src="image-9.png" width="150"> | Không có |

---

## Tổng hợp kết quả

| Chỉ số            | Giá trị |
| ----------------- | ------- |
| Tổng số test case | `9`     |
| Pass              | `7`     |
| Fail              | `2`     |
| Blocked           | `0`     |
| Not Run           | `0`     |
| **Tỷ lệ Pass** | `78%`   |

### Kết quả theo nhóm chức năng

| Nhóm | Tổng TC | Pass | Fail | Tỷ lệ Pass |
| ---- | ------- | ---- | ---- | ---------- |
| REQ-01: Đăng nhập | 5 | 5 | 0 | 100% |
| REQ-07: Quản lý thành viên | 4 | 2 | 2 | 50% |