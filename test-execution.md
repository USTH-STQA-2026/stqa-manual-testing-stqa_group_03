## Kết quả chi tiết (Thành viên C - REQ02 & REQ03)

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| **TC-01** | REQ-02 View Book List | Thẻ sách hiển thị đủ 5 thông tin theo SRS. | Thẻ sách hiện đầy đủ: Tên, Tác giả, Thể loại, Năm XB, Trạng thái. | **Pass** | `N/A` | `N/A` |
| **TC-02** | REQ-02 View Book List | Member xem được danh sách sách. | Member xem danh sách sách bình thường. | **Pass** | <img width="1568" height="1441" alt="image" src="https://github.com/user-attachments/assets/63be7907-3f22-4c75-a819-81839e6cb874" />
 | `N/A` |
| **TC-03** | REQ-02 View Book List | Librarian xem được danh sách sách. | Librarian xem danh sách bình thường. | **Pass** | `N/A` | `N/A` |
| **TC-04** | REQ-02 View Book List | Trạng thái sách cập nhật Real-time. | Trạng thái không tự động đồng bộ khi có người khác mượn sách (phải F5 mới cập nhật). | **Fail** | `evidence/bug_10.png` | `BUG-REQ02-01` |
| **TC-05** | REQ-03 Search Books | Tìm `flutter` ra đúng sách. | Hệ thống hiển thị đúng các sách liên quan. | **Pass** | `N/A` | `N/A` |
| **TC-06** | REQ-03 Search Books | Tìm `FLUTTER` ra kết quả giống chữ thường. | Hệ thống báo trống: "Không tìm thấy sách" (Lỗi phân biệt hoa/thường). | **Fail** | `evidence/bug_c_01.png` | `BUG-10` |
| **TC-07** | REQ-03 Search Books | Tìm kiếm với từ khóa có chứa khoảng trắng thừa ở 2 đầu vẫn ra đúng sách. | Hệ thống báo "Không tìm thấy sách" khi từ khóa có khoảng trắng ở đầu/cuối (Thiếu logic Trim Space). | **Fail** | `evidence/bug_11.png` | `BUG-REQ03-01` |
| **TC-08** | REQ-03 Search Books | Tìm từ khóa ảo báo "Không tìm thấy sách". | Màn hình hiển thị thông báo lỗi chính xác. | **Pass** | `N/A` | `N/A` |
| **TC-09** | REQ-03 Filter Books | Lọc "Công nghệ" và kết hợp tìm kiếm xử lý đúng điều kiện (Logic AND). | Gõ ô tìm kiếm ghi đè và bỏ qua hoàn toàn điều kiện lọc Thể loại đang chọn. | **Fail** | `evidence/bug_12.png` | `BUG-REQ03-02` |
| **TC-10** | REQ-03 Search & Filter | Xóa lọc/tìm kiếm danh sách trở lại ban đầu. | Toàn bộ sách hiển thị lại đầy đủ khi reset. | **Pass** | `N/A` | `N/A` |
