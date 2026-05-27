# Bug Reports — Danh sách báo cáo lỗi chi tiết (Thành viên D)

| Thông tin            |                        |
| -------------------- | ---------------------- |
| **Nhóm** | Nhóm STQA - ICT Gen 15 |
| **Hệ thống phát hiện**| https://stqa.rbc.vn    |
| **Người báo cáo** | Thành viên D           |
| **Tham chiếu** | REQ-05 & REQ-06        |

---

### BUG-REQ05-01: Thiếu cơ chế xác nhận (Popup) và nút Hủy khi chọn Trả sách

* **Mã Test Case liên quan:** TC-05-05
* **Mức độ nghiêm trọng (Severity):** Medium (Lỗi trải nghiệm người dùng - UX Issue)
* **Môi trường lỗi:** Production/Staging (`https://stqa.rbc.vn`)
* **Mô tả chi tiết:** Hệ thống lập tức kích hoạt API và thực hiện hành động trả sách ngay khi người dùng click vào nút "Trả sách". Giao diện hoàn toàn không cung cấp bất kỳ hộp thoại (Popup/Modal) nào bắt hỏi lại để xác nhận hành vi, tước đi quyền hủy bỏ thao tác của người dùng nếu lỡ bấm nhầm.

* **Các bước tái hiện (Steps to Reproduce):**
  1. Đăng nhập vào hệ thống với một tài khoản Thành viên thông thường.
  2. Di chuyển đến danh mục **"Phiếu mượn của tôi"**.
  3. Tìm kiếm một bản ghi phiếu mượn đang ở trạng thái hợp lệ là "Đang mượn".
  4. Thực hiện nhấn chuột vào nút **"Trả sách"** và theo dõi hành vi hệ thống.

* **Kết quả thực tế (Actual Result):** Sách được xử lý trả thành công ngay lập tức mà không cần thông qua bước kiểm tra xác nhận từ phía user.
* **Kết quả mong đợi (Expected Result):** Hệ thống bắt buộc phải hiển thị một Dialog xác nhận với thông điệp: *"Bạn có chắc chắn muốn thực hiện hành động trả cuốn sách này?"* cùng với 2 nút chức năng rõ ràng là **"Xác nhận"** và **"Hủy"**. Nếu nhấp chọn **"Hủy"**, tiến trình phải bị ngắt hoàn toàn và giữ nguyên trạng thái cũ.
* **Minh chứng đính kèm:** `[images/TC-05-05.png]`

---

### BUG-REQ06-01: Bộ lọc trạng thái "Quá hạn" hoạt động sai logic, hiển thị sai dữ liệu

* **Mã Test Case liên quan:** TC-06-03
* **Mức độ nghiêm trọng (Severity):** High (Lỗi sai logic nghiệp vụ hiển thị dữ liệu - Functional Bug)
* **Môi trường lỗi:** Production/Staging (`https://stqa.rbc.vn`)
* **Mô tả chi tiết:** Tại trang quản trị của Thủ thư, khi thực hiện tương tác lọc danh sách các phiếu mượn theo tiêu chí trạng thái là "Quá hạn", thuật toán lọc dữ liệu hoạt động không chính xác khiến kết quả hiển thị bị lẫn lộn, kéo theo cả các phiếu mượn đã hoàn thành nghĩa vụ (trạng thái "Đã trả") vào danh sách hiển thị.

* **Các bước tái hiện (Steps to Reproduce):**
  1. Đăng nhập hệ thống bằng tài khoản quyền Thủ thư (`librarian@library.com`).
  2. Di chuyển đến màn hình chức năng **Quản lý phiếu mượn**.
  3. Tại bộ lọc trạng thái (Dropdown Filter), nhấp chọn duy nhất một giá trị là **"Quá hạn"**.
  4. Xem xét kỹ nhãn trạng thái của từng hàng kết quả vừa trả ra trên bảng dữ liệu.

* **Kết quả thực tế (Actual Result):** Danh sách hiển thị đồng thời cả các bản ghi có nhãn "Quá hạn" xen lẫn các bản ghi có nhãn "Đã trả".
* **Kết quả mong đợi (Expected Result):** Khi bộ lọc "Quá hạn" được áp dụng, hệ thống chỉ được phép xuất ra các phiếu có đúng trạng thái "Quá hạn". Toàn bộ các trạng thái khác (Đang mượn, Đã trả) bắt buộc phải được lọc sạch khỏi màn hình hiển thị.
* **Minh chứng đính kèm:** `[images/TC-06-03.jpeg]`