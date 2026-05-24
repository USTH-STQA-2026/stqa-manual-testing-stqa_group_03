# Test Cases — Bảng trường hợp kiểm thử (Thành viên C)

| Thông tin      |                       |
| -------------- | --------------------- |
| **Nhóm** | Nhóm STQA - ICT Gen 15|
| **Ngày tạo** | 23/05/2026            |
| **Hệ thống** | https://stqa.rbc.vn   |
| **Tham chiếu** | SRS v1.0              |

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

### IDM — Xem danh sách sách (REQ-02)

| Đặc tính (Characteristic)  | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi             |
| -------------------------- | ----------------- | ------------------------ | ---------------------------- |
| Quyền (Role) người dùng    | Thành viên        | `dam.tran@email.com`     | Cho phép truy cập, hiển thị giao diện danh sách thân thiện với người dùng. |
|                            | Thủ thư           | `librarian@email.com`    | Cho phép truy cập, hiển thị danh sách sách đi kèm các công cụ quản trị. |
| Hiển thị thông tin sách    | Đầy đủ các trường | Mã sách: `BOOK001`       | Mỗi thẻ sách hiển thị đủ 5 thông tin: Tên sách, Tác giả, Thể loại, Năm xuất bản, Trạng thái. |
| Đồng bộ dữ liệu            | Thay đổi Real-time| Sách chuyển sang "Đang mượn" | Trạng thái cập nhật tức thì trên màn hình các phiên làm việc khác không cần tải lại trang. |

### IDM — Tìm kiếm & Lọc sách (REQ-03)

| Đặc tính (Characteristic)  | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi             |
| -------------------------- | ----------------- | ------------------------ | ---------------------------- |
| Nhập ký tự tìm kiếm        | Viết thường       | `"flutter"`              | Trả về kết quả chính xác không phân biệt hoa thường. |
|                            | Viết hoa          | `"FLUTTER"`              | Trả về kết quả chính xác không phân biệt hoa thường. |
| Định dạng chuỗi ký tự      | Chứa khoảng trắng | `" Flutter "`            | Hệ thống tự động xóa khoảng trắng thừa (trim space) và tìm đúng sách. |
| Logic bộ lọc Thể loại      | Chọn danh mục     | Thể loại: `"Công nghệ"`  | Danh sách hiển thị thu hẹp, chỉ chứa các sách thuộc đúng thể loại được chọn. |
| Kết hợp Tìm kiếm & Lọc     | Điều kiện AND     | Thể loại: `"Kinh tế"` + Từ khóa: `"Flutter"` | Trả về danh sách trống và hiển thị thông báo "Không tìm thấy sách". |
| Khôi phục danh sách        | Hủy bỏ bộ lọc/tìm | Thực hiện xóa/reset      | Giao diện xóa từ khóa và bộ lọc, tải lại toàn bộ danh sách sách mặc định đầy đủ. |

---

## Bước 2: Bảng chi tiết Test Cases

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi (Strong Oracle) | REQ | Kỹ thuật |
| ----- | ----------------- | -------------- | -------------- | --------------- | ---------------- | --- | -------- |
| **TC-02-01** | Xem danh sách – Kiểm tra độ hiển thị đầy đủ các trường UI | Đăng nhập hệ thống bằng một tài khoản bất kỳ. | 1. Truy cập vào trang chủ hệ thống.<br