## Kết quả chi tiết (Thành viên C - REQ02 & REQ03)

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| **TC-02-01** | REQ-02 View Book List | Thẻ sách hiển thị đủ 5 thông tin theo SRS. | Thẻ sách hiện đầy đủ: Tên, Tác giả, Thể loại, Năm XB, Trạng thái. | **Pass** | `N/A` | `N/A` |
| **TC-02-02** | REQ-02 View Book List | Member xem được danh sách sách. | Member xem danh sách sách bình thường. | **Pass** | `N/A` | `N/A` |
| **TC-02-03** | REQ-02 View Book List | Librarian xem được danh sách sách. | Librarian xem danh sách bình thường. | **Pass** | `N/A` | `N/A` |
| **TC-02-04** | REQ-02 View Book List | Trạng thái sách cập nhật Real-time. | Trạng thái không tự động đồng bộ khi có người khác mượn sách (phải F5 mới cập nhật). | **Fail** | `evidence/bug_10.png` | `BUG-REQ02-01` |
| **TC-03-01** | REQ-03 Search Books | Tìm `flutter` ra đúng sách. | Hệ thống hiển thị đúng các sách liên quan. | **Pass** | `N/A` | `N/A` |
| **TC-03-02** | REQ-03 Search Books | Tìm `FLUTTER` ra kết quả giống chữ thường. | Hệ thống xử lý không phân biệt hoa/thường, hiển thị đúng sách. | **Pass** | `N/A` | `N/A` |
| **TC-03-03** | REQ-03 Search Books | Tìm kiếm với từ khóa có khoảng trắng ở 2 đầu ra đúng sách. | Hệ thống báo "Không tìm thấy sách" khi từ khóa có khoảng trắng ở đầu/cuối. | **Fail** | `evidence/bug_11.png` | `BUG-REQ03-01` |
| **TC-03-04** | REQ-03 Filter Books | Thu hẹp danh sách bằng bộ lọc Thể loại "Công nghệ". | Hệ thống lọc chuẩn xác, chỉ hiển thị sách Công nghệ. | **Pass** | `N/A` | `N/A` |
| **TC-03-05** | REQ-03 Search & Filter| Lọc "Kinh tế" và kết hợp tìm kiếm "Flutter" (Logic AND). | Gõ ô tìm kiếm ghi đè và bỏ qua hoàn toàn điều kiện lọc Thể loại đang chọn. | **Fail** | `evidence/bug_12.png` | `BUG-REQ03-02` |
| **TC-03-06** | REQ-03 Search & Filter| Xóa lọc/tìm kiếm danh sách trở lại ban đầu. | Toàn bộ sách hiển thị lại đầy đủ khi reset. | **Pass** | `N/A` | `N/A` |