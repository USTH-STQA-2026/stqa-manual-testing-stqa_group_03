# Test cases – Thành viên D (REQ-05 & REQ-06)

## REQ-05: Trả sách

| Mã TC | Mục tiêu | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | Kỹ thuật |
|-------|----------|----------------|----------------|------------------|------------------|-----------|
| **TC-05-01** | Trả sách đúng hạn – thành công, không cảnh báo | Đăng nhập thành viên. Có 1 phiếu mượn còn hạn. | 1. Vào "Phiếu mượn của tôi"<br>2. Chọn phiếu chưa quá hạn<br>3. Nhấn "Trả sách"<br>4. Xác nhận | Mã phiếu bất kỳ | • Thông báo "Trả sách thành công"<br>• Sách biến mất khỏi danh sách đang mượn<br>• Sách hiện "Có sẵn" trong kho<br>• Không cảnh báo quá hạn | Happy path |
| **TC-05-02** | Trả sách quá hạn – thành công, có cảnh báo | Đăng nhập thành viên. Có phiếu mượn quá hạn (hạn trả < hôm nay). | Giống TC-05-01 (chọn phiếu quá hạn) | Mã phiếu quá hạn | • Trả thành công<br>• Có cảnh báo "Sách trả quá hạn"<br>• Trạng thái sách được cập nhật | Negative / Cảnh báo |
| **TC-05-03** | Trả sách đã trả rồi – hệ thống từ chối ẩn nút | Có phiếu mượn đã được trả (sau TC-05-01). | 1. Vào "Lịch sử mượn"<br>2. Tìm phiếu đã trả và kiểm tra thao tác | Mã phiếu đã trả | • Hệ thống không hiển thị nút "Trả sách" trên phiếu đã trả để ngăn chặn thao tác trùng lặp | Biên / UX |
| **TC-05-04** | Trả sách khi chưa đăng nhập – chuyển hướng login | Chưa đăng nhập (trình duyệt ẩn danh). | 1. Mở cửa sổ ẩn danh<br>2. Truy cập URL trả sách (nếu biết)<br>3. Quan sát | Không | • Chuyển hướng về trang đăng nhập<br>• Hoặc thông báo "Vui lòng đăng nhập" | Bảo mật |
| **TC-05-05** | Hủy thao tác trả sách – không thay đổi | Đăng nhập thành viên, có phiếu đang mượn. | 1. Vào "Phiếu mượn của tôi"<br>2. Nhấn "Trả sách"<br>3. Trong hộp thoại xác nhận, chọn **Hủy** | Mã phiếu đang mượn | • Hộp thoại đóng lại<br>• Phiếu vẫn ở trạng thái "Đang mượn"<br>• Sách chưa bị trả | Giao diện |

## REQ-06: Xử lý quá hạn

| Mã TC | Mục tiêu | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | Kỹ thuật |
|-------|----------|----------------|----------------|------------------|------------------|-----------|
| **TC-06-01** | Thủ thư nhấn "Kiểm tra quá hạn" – tự động cập nhật phiếu | Đăng nhập thủ thư (`librarian@library.com`). Hệ thống có phiếu mượn BR001 đã quá hạn nhưng chưa quét. | 1. Vào trang quản lý phiếu mượn<br>2. Tìm nút "Kiểm tra quá hạn"<br>3. Nhấn nút | Mã phiếu: BR001 | • Thông báo: "Đã cập nhật X phiếu quá hạn" (X≥1)<br>• Hệ thống quét tự động, chuyển trạng thái phiếu BR001 từ "Đang mượn" → "Quá hạn" | Happy path |
| **TC-06-02** | Kiểm tra quá hạn khi không có phiếu quá hạn | Đăng nhập thủ thư. Tất cả phiếu đều còn hạn hoặc đã trả. | Giống TC-06-01 | Hệ thống sạch (không có phiếu quá hạn) | • Thông báo: "Không có phiếu quá hạn" hoặc "0 phiếu"<br>• Không thay đổi trạng thái của bất kỳ phiếu nào | Biên / Xử lý rỗng |
| **TC-06-03** | Lọc danh sách phiếu theo trạng thái "Quá hạn" | Sau TC-06-01, có ít nhất 1 phiếu quá hạn. Đăng nhập thủ thư. | 1. Trên trang quản lý phiếu mượn, chọn bộ lọc "Quá hạn"<br>2. Xem kết quả | Bộ lọc: "Quá hạn" | • Danh sách chỉ hiển thị phiếu có trạng thái "Quá hạn"<br>• Các phiếu thuộc trạng thái khác (Đang mượn, Đã trả) bị ẩn đi | Giao diện |
| **TC-06-04** | Thành viên thấy phiếu của mình bị đánh dấu "Quá hạn" | Sau TC-06-01, thành viên A có phiếu đã bị đánh dấu "Quá hạn". | 1. Đăng xuất thủ thư<br>2. Đăng nhập bằng tài khoản thành viên A<br>3. Vào "Phiếu mượn của tôi" | Tài khoản thành viên A | • Phiếu hiển thị trạng thái "Quá hạn" (màu đỏ, nổi bật)<br>• Ngày hạn trả được làm nổi bật | Đa vai trò |
| **TC-06-05** | Thành viên không có quyền truy cập "Kiểm tra quá hạn" | Đăng nhập tài khoản thành viên thường . | 1. Tìm nút "Kiểm tra quá hạn" trên giao diện<br>2. Thử truy cập trực tiếp URL quét quá hạn | Không | • Nút không hiển thị trên giao diện thành viên<br>• Truy cập trực tiếp qua URL → báo lỗi 403 hoặc chuyển hướng | Bảo mật / Phân quyền |