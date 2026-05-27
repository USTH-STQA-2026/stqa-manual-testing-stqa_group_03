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
| **TC-02-01** | Xem danh sách – Kiểm tra độ hiển thị đầy đủ các trường UI | Đăng nhập hệ thống bằng một tài khoản bất kỳ. | 1. Truy cập vào trang chủ hệ thống.<br>2. Quan sát một thẻ sách bất kỳ hiển thị trên giao diện (ví dụ mã BOOK001). | Tài khoản hợp lệ | Mỗi thẻ sách hiển thị rõ ràng và đầy đủ 5 trường thông tin bắt buộc: Tên sách, Tác giả, Thể loại, Năm xuất bản và Trạng thái. | REQ-02 | Happy path / UI |
| **TC-02-02** | Xem danh sách dưới giao diện vai trò Thành viên | Đăng nhập tài khoản vai trò Thành viên. | 1. Truy cập vào màn hình trang chủ hệ thống.<br>2. Kiểm tra khả năng hiển thị tổng quan danh sách sách. | `dam.tran@email.com` | Danh sách sách hiển thị bình thường, giao diện sạch sẽ, thân thiện và tối ưu cho việc tìm kiếm, mượn sách của Thành viên. | REQ-02 | Happy path / Phân quyền |
| **TC-02-03** | Xem danh sách dưới giao diện vai trò Thủ thư | Đăng nhập tài khoản vai trò Thủ thư. | 1. Di chuyển đến màn hình chức năng quản lý sách.<br>2. Kiểm tra khả năng hiển thị danh sách sách. | `librarian@email.com` | Danh sách sách hiển thị đầy đủ, chi tiết và có đi kèm các nút tính năng/công cụ quản trị hệ thống dành riêng cho Thủ thư. | REQ-02 | Happy path / Phân quyền |
| **TC-02-04** | Xem danh sách – Kiểm tra đồng bộ dữ liệu trạng thái theo thời gian thực (Real-time) | Có 2 tài khoản đăng nhập đồng thời trên hai thiết bị/phiên trình duyệt độc lập. | 1. Tại tài khoản Thành viên, thực hiện bấm mượn cuốn sách `BOOK003`.<br>2. Tại tài khoản Thủ thư, quan sát trạng thái sách trên màn hình mà không tải lại trang. | Mã sách: `BOOK003` | Trạng thái của cuốn sách `BOOK003` trên màn hình Thủ thư ngay lập tức tự động cập nhật chuyển từ "Có sẵn" sang "Đang mượn" (không cần nhấn F5). | REQ-02 | Real-time / Đồng bộ dữ liệu |
| **TC-03-01** | Tìm kiếm sách bằng từ khóa viết thường | Đăng nhập hệ thống, đang ở màn hình trang chủ. | 1. Nhập từ khóa chữ thường `"flutter"` vào thanh ô tìm kiếm.<br>2. Nhấn phím Enter hoặc nhấp chọn biểu tượng tìm kiếm. | Từ khóa: `"flutter"` | Hệ thống lọc chính xác và hiển thị cuốn sách phù hợp là "Lập trình Flutter cơ bản" lên màn hình. | REQ-03 | Happy path / Search |
| **TC-03-02** | Tìm kiếm sách bằng từ khóa viết hoa (Không phân biệt hoa thường) | Đăng nhập hệ thống, đang ở màn hình trang chủ. | 1. Nhập từ khóa chữ hoa toàn bộ `"FLUTTER"` vào thanh ô tìm kiếm.<br>2. Thực hiện hành động tìm kiếm. | Từ khóa: `"FLUTTER"` | Hệ thống xử lý không phân biệt hoa thường, trả về kết quả chính xác cuốn sách "Lập trình Flutter cơ bản". | REQ-03 | Robustness / Search |
| **TC-03-03** | Tìm kiếm sách với từ khóa đầu vào chứa khoảng trắng ở đầu và cuối chuỗi (Trim Space) | Đăng nhập hệ thống, đang ở màn hình trang chủ. | 1. Nhập chuỗi từ khóa có dấu cách dư thừa ở hai đầu: `" Flutter "` vào ô tìm kiếm.<br>2. Nhấn tìm kiếm và xem kết quả. | Từ khóa: `" Flutter "` | Hệ thống tự động cắt bỏ (trim) các khoảng trắng dư thừa, thực hiện truy vấn gốc và hiển thị đúng cuốn sách "Lập trình Flutter cơ bản". | REQ-03 | Biên / Xử lý chuỗi |
| **TC-03-04** | Thu hẹp danh sách bằng bộ lọc Thể loại sách | Đăng nhập hệ thống, đang ở màn hình trang chủ. | 1. Tại thanh công cụ lọc Thể loại sách, nhấp chọn danh mục `"Công nghệ"`.<br>2. Quan sát danh sách kết quả hiển thị. | Bộ lọc: `"Công nghệ"` | Hệ thống lọc chuẩn xác, chỉ hiển thị những cuốn sách có nhãn thuộc thể loại Công nghệ, không bị lọt các thể loại khác. | REQ-03 | Happy path / Filter |
| **TC-03-05** | Tìm kiếm từ khóa kết hợp điều kiện lọc Thể loại không liên quan (Xung đột Search & Filter) | Đăng nhập hệ thống, đang ở màn hình trang chủ. | 1. Nhấp kích hoạt bộ lọc Thể loại là `"Kinh tế"`.<br>2. Tại ô tìm kiếm, nhập từ khóa sách công nghệ: `"Flutter"`.<br>3. Tiến hành thực thi truy vấn tìm kiếm. | Thể loại: `"Kinh tế"`, Từ khóa: `"Flutter"` | Hệ thống áp dụng logic toán tử AND đồng thời. Vì sách Flutter không thuộc nhóm Kinh tế, kết quả phải hiển thị trống kèm thông báo "Không tìm thấy sách". | REQ-03 | Logic nghiệp vụ / AND |
| **TC-03-06** | Xóa từ khóa tìm kiếm và bộ lọc để khôi phục danh sách mặc định | Hệ thống đang ở trạng thái hiển thị danh sách đã lọc/tìm kiếm thu hẹp. | 1. Tiến hành xóa trắng ký tự trong ô tìm kiếm.<br>2. Click hủy chọn bộ lọc Thể loại đang kích hoạt.<br>3. Quan sát lại giao diện. | Thao tác: Click Reset / Clear | Thanh tìm kiếm rỗng, các bộ lọc được bỏ chọn; hệ thống tự động tải và hiển thị lại toàn bộ danh sách sách mặc định ban đầu một cách đầy đủ. | REQ-03 | Giao diện / Reset |

---

## Bước 3: Tổng hợp độ bao phủ

| Nhóm chức năng       | Số TC | REQ phủ | Kỹ thuật IDM áp dụng                                            |
| -------------------- | ----- | ------- | --------------------------------------------------------------- |
| Xem danh sách sách   | 4     | REQ-02  | Phân lớp tương đương (EP), Phân quyền người dùng, Cập nhật Real-time |
| Tìm kiếm & Lọc sách  | 6     | REQ-03  | Phân lớp tương đương (EP), Kiểm thử giá trị biên (BVA), Logic nghiệp vụ phối hợp |
| **Tổng cộng** | **10**| **2 REQs**|                                                                 |