# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Viết tối thiểu **20 TC** phủ đủ các chức năng chính (REQ-01 → REQ-08).
> Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.
> Tự tổ chức và phân nhóm test case theo cách hợp lý nhất.

| Thông tin | |
|---|---|
| **Nhóm** | `<!-- Tên nhóm -->` |
| **Ngày tạo** | `<!-- DD/MM/YYYY -->` |
| **Hệ thống** | https://stqa.rbc.vn |
| **Tham chiếu** | SRS v1.0 |

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

> 📖 **Textbook:** Chương 6 — *Input Domain Modeling*, Paul Ammann & Jeff Offutt.
>
> **Trước khi viết Test Case**, nhóm **phải** phân tích miền đầu vào bằng bảng IDM bên dưới.
> Mỗi chức năng cần xác định: **Đặc tính (Characteristic)**, **Phân vùng (Block/Partition)**, và **Giá trị đại diện (Value)**.

### IDM — Đăng nhập (REQ-01)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Email có tồn tại trong DB? | Có | `librarian@library.com` | Đăng nhập thành công |
| | Không | `noone@email.com` | Thông báo lỗi |
| Mật khẩu có đúng? | Đúng | `admin123` | Đăng nhập thành công |
| | Sai | `wrongpass` | Thông báo lỗi |
| Ô nhập có rỗng? | Không rỗng | (giá trị bất kỳ) | Xử lý bình thường |
| | Rỗng | `""` | Thông báo "Vui lòng nhập..." |

### IDM — Tìm kiếm sách (REQ-03)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Từ khóa có tồn tại trong DB? | Có (tên sách) | `"Flutter"` | Hiển thị sách chứa "Flutter" |
| | Có (tên tác giả) | `"Nguyễn"` | Hiển thị sách của tác giả Nguyễn |
| | Không | `"XYZ123"` | Danh sách rỗng |
| Phân biệt HOA/thường? | Chữ thường | `"flutter"` | Kết quả giống "Flutter" |
| | Chữ HOA | `"FLUTTER"` | Kết quả giống "Flutter" |

### IDM — Mượn sách (REQ-04, REQ-05)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Trạng thái sách? | Có sẵn | BOOK001 | Cho phép mượn |
| | Đang mượn | BOOK003 | Không cho phép |
| | Thất lạc | BOOK007 | Không cho phép |
| Trạng thái thành viên? | Hoạt động | MEM002 | Cho phép mượn |
| | Tạm ngưng | MEM004 | Từ chối, thông báo lỗi |
| | Hết hạn | MEM005 | Từ chối, thông báo lỗi |
| Số sách đang mượn? | < 3 (BVA: 0, 1, 2) | MEM006 (0 sách) | Cho phép mượn |
| | = 3 (BVA: giới hạn) | MEM đã mượn 3 sách | Từ chối, thông báo vượt giới hạn |

### IDM — `<!-- Nhóm tự bổ sung cho REQ-05 đến REQ-08 -->`

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| `<!-- Nhóm tự điền -->` | | | |

> 💡 **Gợi ý kỹ thuật**: Sử dụng **Phân lớp tương đương (EP)** cho các phân vùng rời rạc, **Phân tích giá trị biên (BVA)** cho các phân vùng số (ví dụ: giới hạn 3 sách). Xem textbook §6.1–6.3.

---

## Bước 2: Bảng chi tiết Test Cases

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi (Strong Oracle) | REQ | Kỹ thuật |
|---|---|---|---|---|---|---|---|
| **TC-02-01** | Xem danh sách – Kiểm tra độ hiển thị đầy đủ các trường UI | Đăng nhập hệ thống bằng một tài khoản bất kỳ. | 1. Truy cập vào trang chủ hệ thống.<br>2. Quan sát thẻ sách bất kỳ (vd: BOOK001). | Tài khoản hợp lệ | Mỗi thẻ sách hiển thị đủ 5 thông tin: Tên sách, Tác giả, Thể loại, Năm xuất bản, Trạng thái. | REQ-02 | Giao diện (UI) |
| **TC-02-02** | Xem danh sách – Kiểm tra hiển thị đối với vai trò Thành viên | Đăng nhập bằng tài khoản Thành viên. | 1. Truy cập trang chủ hệ thống.<br>2. Kiểm tra giao diện danh sách sách. | `dam.tran@email.com` | Danh sách hiển thị bình thường, giao diện được tối ưu cho Thành viên mượn sách. | REQ-02 | Phân quyền (Role-based) |
| **TC-02-03** | Xem danh sách – Kiểm tra hiển thị đối với vai trò Thủ thư | Đăng nhập bằng tài khoản Thủ thư. | 1. Di chuyển đến mục quản lý sách.<br>2. Kiểm tra giao diện danh sách. | `librarian@email.com` | Danh sách hiển thị đầy đủ, đi kèm các công cụ quản trị dành riêng cho Thủ thư. | REQ-02 | Phân quyền (Role-based) |
| **TC-02-04** | Xem danh sách – Kiểm tra đồng bộ trạng thái sách (Real-time) | 2 tài khoản đăng nhập trên 2 phiên làm việc độc lập. | 1. Tại TK Thành viên, mượn sách `BOOK003`.<br>2. Tại TK Thủ thư, quan sát trạng thái sách (không F5). | Sách: `BOOK003` | Trạng thái cuốn `BOOK003` trên màn hình Thủ thư lập tức đổi sang "Đang mượn" (không cần F5). | REQ-02 | Kiểm thử chức năng / Real-time |
| **TC-03-01** | Tìm kiếm sách bằng từ khóa viết thường | Đang ở trang chủ hệ thống. | 1. Nhập từ khóa chữ thường vào ô tìm kiếm.<br>2. Nhấn Enter. | `"flutter"` | Hệ thống trả về đúng cuốn sách "Lập trình Flutter cơ bản". | REQ-03 | Happy Path / EP |
| **TC-03-02** | Tìm kiếm sách không phân biệt chữ hoa/thường | Đang ở trang chủ hệ thống. | 1. Nhập từ khóa viết hoa toàn bộ.<br>2. Nhấn Enter. | `"FLUTTER"` | Hệ thống không phân biệt hoa/thường, trả về đúng cuốn sách "Lập trình Flutter cơ bản". | REQ-03 | Phân lớp tương đương (EP) |
| **TC-03-03** | Tự động xóa khoảng trắng ở 2 đầu từ khóa (Trim Space) | Đang ở trang chủ hệ thống. | 1. Nhập từ khóa có dấu cách thừa ở đầu và cuối.<br>2. Nhấn Enter. | `" Flutter "` | Hệ thống tự động cắt bỏ khoảng trắng (trim) và tìm đúng cuốn sách "Lập trình Flutter cơ bản". | REQ-03 | Kiểm thử giá trị biên (BVA) / Xử lý chuỗi |
| **TC-03-04** | Lọc danh sách sách theo Thể loại | Đang ở trang chủ hệ thống. | 1. Mở Dropdown bộ lọc Thể loại.<br>2. Chọn một danh mục. | Thể loại: `"Công nghệ"` | Danh sách chỉ hiển thị những cuốn sách thuộc thể loại Công nghệ, không lọt sách khác vào. | REQ-03 | Happy Path / EP |
| **TC-03-05** | Xung đột khi tìm kiếm kết hợp bộ lọc không liên quan | Đang ở trang chủ hệ thống. | 1. Chọn bộ lọc Thể loại là "Kinh tế".<br>2. Gõ từ khóa tìm kiếm sách công nghệ.<br>3. Nhấn Enter. | Filter: `"Kinh tế"`<br>Search: `"Flutter"` | Kết hợp bằng toán tử AND: Hệ thống báo "Không tìm thấy sách" (do Flutter không thuộc mảng Kinh tế). | REQ-03 | Bảng quyết định (Decision Table) |
| **TC-03-06** | Hủy điều kiện lọc/tìm kiếm để xem lại toàn bộ sách | Đang ở màn hình hiển thị kết quả tìm kiếm/lọc. | 1. Xóa chữ trong ô tìm kiếm.<br>2. Hủy chọn bộ lọc Thể loại. | Thao tác Xóa / Reset | Hệ thống lập tức tự động tải và hiển thị lại toàn bộ danh sách sách mặc định ban đầu. | REQ-03 | Chuyển đổi trạng thái (State Transition) |