# Bug Reports — Danh sách báo cáo lỗi chi tiết (Thành viên C)

### BUG-REQ02-01: Trạng thái mượn sách không tự động cập nhật theo thời gian thực giữa các phiên làm việc
* **Mã Test Case liên quan:** TC-04
* **Mức độ nghiêm trọng (Severity):** Medium (Lỗi chức năng không đồng bộ dữ liệu thời gian thực - Functional Issue)
* **Môi trường lỗi:** Production/Staging (`https://stqa.rbc.vn`)
* **Mô tả chi tiết:** Trạng thái khả dụng của tài liệu không tự động đồng bộ hóa tức thời giữa các tài khoản người dùng đang đăng nhập đồng thời trên hệ thống. Khi có người mượn tài liệu thành công, các phiên làm việc khác không nhận được cập nhật cho đến khi thực hiện tải lại trang theo cách thủ công.
* **Các bước tái hiện (Steps to Reproduce):**
  1. Đăng nhập hệ thống đồng thời bằng 2 phiên làm việc khác nhau: Phiên 1 bằng tài khoản Thủ thư (`librarian@email.com`), Phiên 2 bằng tài khoản Thành viên (`dam.tran@email.com`).
  2. Tại cả 2 phiên, cùng mở màn hình trang chủ và quan sát cuốn sách mang mã số `BOOK001` (Trạng thái hiện tại trên màn hình là "Có sẵn").
  3. Tại phiên 2 (Thành viên), thực hiện nhấn nút mượn cuốn sách `BOOK001`.
  4. Quay lại màn hình của phiên 1 (Thủ thư) và quan sát trạng thái của cuốn sách `BOOK001` mà không thực hiện hành động tải lại trang (F5).
* **Kết quả thực tế (Actual Result):** Trên màn hình của Thủ thư, trạng thái cuốn sách `BOOK001` vẫn giữ nguyên trạng thái cũ là "Có sẵn".
* **Kết quả mong đợi (Expected Result):** Hệ thống phải tự động đồng bộ dữ liệu tức thì theo thời gian thực (Real-time), chuyển trạng thái cuốn sách `BOOK001` trên màn hình Thủ thư sang "Đang mượn" mà không cần tải lại trang.
* **Minh chứng đính kèm:** `[evidence/bug_10.png]`

---

### BUG-REQ03-01: Hệ thống xử lý sai truy vấn khi từ khóa chứa khoảng trắng ở đầu hoặc cuối (Thiếu logic Trim Space)
* **Mã Test Case liên quan:** TC-07
* **Mức độ nghiêm trọng (Severity):** Medium (Lỗi xử lý định dạng dữ liệu đầu vào - Input Handling Bug)
* **Môi trường lỗi:** Production/Staging (`https://stqa.rbc.vn`)
* **Mô tả chi tiết:** Thanh tìm kiếm không thực hiện xử lý chuẩn hóa chuỗi đầu vào (Cắt bỏ khoảng trắng thừa ở 2 đầu). Khi người dùng nhập từ khóa có chứa dấu cách ở đầu/cuối, hệ thống bị lỗi logic truy vấn, dẫn đến việc bỏ qua từ khóa và tải lại toàn bộ danh sách sách mặc định ban đầu.
* **Các bước tái hiện (Steps to Reproduce):**
  1. Truy cập vào trang chủ hệ thống bằng một tài khoản Thành viên hợp lệ.
  2. Tại ô tìm kiếm sách, nhập chuỗi từ khóa có chứa khoảng trắng ở cả hai đầu: `" Flutter "` (có dấu cách phía trước và dấu cách phía sau chữ Flutter).
  3. Nhấn phím Enter hoặc biểu tượng tìm kiếm để thực thi truy vấn.
* **Kết quả thực tế (Actual Result):** Hệ thống không thông báo "Không tìm thấy sách", mà thay vào đó hiển thị toàn bộ danh sách sách có trong thư viện (Bao gồm cả Cấu trúc dữ liệu, Mạng máy tính,...).
* **Kết quả mong đợi (Expected Result):** Hệ thống phải tự động loại bỏ (trim) các khoảng trắng dư thừa ở đầu và cuối chuỗi ký tự trước khi thực hiện truy vấn và trả về kết quả chính xác duy nhất là cuốn sách "Lập trình Flutter cơ bản".
* **Minh chứng đính kèm:** `[image_0d9f83.png]`

---

### BUG-REQ03-02: Ô tìm kiếm ghi đè và bỏ qua hoàn toàn điều kiện lọc của Thể loại sách (Xung đột Search & Filter)
* **Mã Test Case liên quan:** TC-09
* **Mức độ nghiêm trọng (Severity):** High (Lỗi sai logic nghiệp vụ kết hợp điều kiện lọc - Functional Bug)
* **Môi trường lỗi:** Production/Staging (`https://stqa.rbc.vn`)
* **Mô tả chi tiết:** Hệ thống không áp dụng đồng thời (logic toán tử AND) giữa bộ lọc Thể loại và Ô tìm kiếm từ khóa. Khi người dùng đang chọn một Thể loại cụ thể, việc gõ từ khóa tìm kiếm sẽ ghi đè hoàn toàn bộ lọc này, dẫn đến hiển thị kết quả sai lệch với điều kiện danh mục đang chọn.
* **Các bước tái hiện (Steps to Reproduce):**
  1. Tại thanh công cụ lọc của giao diện trang chủ, nhấp chọn bộ lọc Thể loại là **"Kinh tế"**.
  2. Tại ô tìm kiếm sách, nhập vào từ khóa của một cuốn sách thuộc thể loại Công nghệ: **"Flutter"**.
  3. Tiến hành thực thi tìm kiếm và quan sát danh sách kết quả hiển thị trên màn hình.
* **Kết quả thực tế (Actual Result):** Giao diện vẫn hiển thị đang lọc "Kinh tế", nhưng hệ thống lại trả về cuốn sách "Lập trình Flutter cơ bản" (có nhãn thể loại là Công nghệ).
* **Kết quả mong đợi (Expected Result):** Hệ thống phải áp dụng kết hợp đồng thời cả hai điều kiện lọc (Thể loại = Kinh tế AND Từ khóa = Flutter). Do sách Flutter thuộc nhóm Công nghệ chứ không phải Kinh tế, hệ thống bắt buộc phải hiển thị trống và thông báo "Không tìm thấy sách".
* **Minh chứng đính kèm:** `[image_0da2e9.png]`