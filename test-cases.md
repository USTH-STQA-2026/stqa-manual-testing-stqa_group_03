# Step 1: Input Domain Modeling (IDM)

## ## IDM – View Book List (REQ-02)

| Characteristic | Block / Partition | Representative Value | Expected Result |
|---|---|---|---|
| User role visibility | Member | `dam.tran@email.com` | Display book list with 5 required fields |
| | Librarian | `librarian@email.com` | Display book list with 5 required fields and administrative tools |
| Book information fields | Complete fields | `BOOK001` | Show Title, Author, Category, Publish Year, Status |
| Real-time state change | Book status modified | `BOOK003` changes to Borrowed | Status updates on screen instantly without reloading |

## ## IDM – Search & Filter Books (REQ-03)

| Characteristic | Block / Partition | Representative Value | Expected Result |
|---|---|---|---|
| Search case sensitivity | Lowercase / Uppercase | `flutter` / `FLUTTER` | Display matching books (Case-insensitive) |
| Search input format | Contains trailing/leading spaces | `" Flutter "` | System trims spaces and displays matching books |
| Category filter logic | Valid category selection | `Công nghệ` | Display books belonging only to selected category |
| Search & Filter combination | Filter applied + Unrelated Search | Filter `Kinh tế` + Search `Flutter` | Display empty result "Không tìm thấy sách" |

---

# Step 2: Test Cases (Thành viên C)

## ## Test Cases – REQ-02 View Book List

### TC-01: Verify book list UI fields completeness
* **Yêu cầu:** REQ-02 (View Book List)
* **Loại kiểm thử:** Happy Path
* **Mô tả:** Đảm bảo hệ thống hiển thị đầy đủ 5 trường thông tin bắt buộc cho mỗi cuốn sách theo tài liệu SRS.
* **Các bước thực hiện:**
  1. Truy cập hệ thống và đăng nhập.
  2. Quan sát giao diện thẻ sách ở trang chủ.
* **Dữ liệu đầu vào:** Tài khoản hợp lệ.
* **Kết quả mong đợi:** Mỗi thẻ sách hiển thị đủ 5 thông tin: Tên sách, Tác giả, Thể loại, Năm xuất bản và Trạng thái.

### TC-02: Verify book list accessibility for Member role
* **Yêu cầu:** REQ-02 (View Book List)
* **Loại kiểm thử:** Permission
* **Mô tả:** Xác minh tài khoản Member có quyền xem danh sách sách.
* **Các bước thực hiện:** Đăng nhập bằng tài khoản Member và kiểm tra trang chủ.
* **Dữ liệu đầu vào:** `ba.nguyen@email.com` / `password123`
* **Kết quả mong đợi:** Hiển thị danh sách sách dành cho Thành viên.

### TC-03: Verify book list accessibility for Librarian role
* **Yêu cầu:** REQ-02 (View Book List)
* **Loại kiểm thử:** Permission
* **Mô tả:** Xác minh tài khoản Librarian có quyền xem danh sách.
* **Các bước thực hiện:** Đăng nhập bằng tài khoản Librarian và kiểm tra trang chủ.
* **Dữ liệu đầu vào:** `librarian@email.com` / `admin123`
* **Kết quả mong đợi:** Hiển thị danh sách sách kèm các công cụ quản lý.

### TC-04: Verify real-time status update on borrow action
* **Yêu cầu:** REQ-02 (View Book List)
* **Loại kiểm thử:** Real-time update
* **Mô tả:** Trạng thái sách tự động cập nhật ngay lập tức khi có người mượn mà không cần tải lại trang.
* **Các bước thực hiện:**
  1. Mở 2 tab. Tab 1 đăng nhập Librarian, Tab 2 đăng nhập Member.
  2. Tại Tab 2, bấm Mượn cuốn `BOOK001`.
  3. Quan sát Tab 1 (Không F5).
* **Dữ liệu đầu vào:** Mượn sách `BOOK001`.
* **Kết quả mong đợi:** Trạng thái cuốn `BOOK001` ở Tab 1 tự động chuyển sang "Đang mượn".

---

## ## Test Cases – REQ-03 Search & Filter Books

### TC-05: Search book with standard keywords
* **Yêu cầu:** REQ-03 (Search Books)
* **Loại kiểm thử:** Happy Path
* **Mô tả:** Hệ thống tìm kiếm đúng sách khi nhập từ khóa bình thường.
* **Các bước thực hiện:** Nhập từ khóa vào ô tìm kiếm và nhấn Enter.
* **Dữ liệu đầu vào:** `flutter`
* **Kết quả mong đợi:** Hiển thị các sách có chứa từ "Flutter".

### TC-06: Search book with UPPERCASE keyword
* **Yêu cầu:** REQ-03 (Search Books)
* **Loại kiểm thử:** Equivalence Partitioning
* **Mô tả:** Hệ thống không phân biệt chữ hoa/thường.
* **Các bước thực hiện:** Nhập từ khóa IN HOA.
* **Dữ liệu đầu vào:** `FLUTTER`
* **Kết quả mong đợi:** Trả về kết quả giống TC-05.

### TC-07: Search book with leading and trailing spaces
* **Yêu cầu:** REQ-03 (Search Books)
* **Loại kiểm thử:** Exception Handling / Data Formatting
* **Mô tả:** Hệ thống phải tự động xóa khoảng trắng thừa ở đầu/cuối từ khóa trước khi tìm kiếm.
* **Các bước thực hiện:**
  1. Nhập từ khóa có chứa dấu cách ở đầu và cuối.
  2. Nhấn Enter.
* **Dữ liệu đầu vào:** `" Flutter "` (Có dấu cách 2 bên).
* **Kết quả mong đợi:** Hệ thống tự động trim khoảng trắng và hiển thị danh sách sách "Flutter".

### TC-08: Filter books by a valid Category
* **Yêu cầu:** REQ-03 (Filter Books)
* **Loại kiểm thử:** Happy Path
* **Mô tả:** Bộ lọc phân loại hoạt động chính xác.
* **Các bước thực hiện:** Chọn một thể loại từ Dropdown.
* **Dữ liệu đầu vào:** Thể loại `Công nghệ`.
* **Kết quả mong đợi:** Chỉ hiển thị các cuốn sách thuộc thể loại "Công nghệ".

### TC-09: Filter and Search conflict handling
* **Yêu cầu:** REQ-03 (Search & Filter)
* **Loại kiểm thử:** Logic / Edge Case
* **Mô tả:** Kiểm tra logic kết hợp giữa tìm kiếm và lọc thể loại.
* **Các bước thực hiện:**
  1. Chọn bộ lọc Thể loại là `Kinh tế`.
  2. Tại ô tìm kiếm, gõ từ khóa của sách Công nghệ.
* **Dữ liệu đầu vào:** Filter `Kinh tế` + Search `Flutter`.
* **Kết quả mong đợi:** Hệ thống báo "Không tìm thấy sách" (Do sách Flutter không thuộc thể loại Kinh tế).

### TC-10: Reset Filter and Search to display full book list
* **Yêu cầu:** REQ-03 (Search & Filter)
* **Loại kiểm thử:** State Reset
* **Mô tả:** Danh sách quay về trạng thái đầy đủ sau khi xóa tìm kiếm/lọc.
* **Các bước thực hiện:** Xóa tìm kiếm và Reset dropdown bộ lọc.
* **Dữ liệu đầu vào:** Clear inputs.
* **Kết quả mong đợi:** Hiển thị lại toàn bộ danh sách sách.