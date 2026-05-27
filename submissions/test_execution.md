# Test Execution Report — Kết quả thực thi kiểm thử (Thành viên D)

| Thông tin            |                        |
| -------------------- | ---------------------- |
| **Nhóm** | Nhóm STQA - ICT Gen 15 |
| **Ngày chạy thực tế**| 23/05/2026            |
| **Hệ thống test** | https://stqa.rbc.vn    |
| **Người thực hiện** | Thành viên D           |

---

## 1. Bảng kết quả thực thi chi tiết (REQ-05 & REQ-06)

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Mã Bug (Xem chi tiết tại bug_reports.md) |
|---|---|---|---|---|---|---|
| **TC-05-01** | Trả sách | Trả thành công, sách thành "Có sẵn", không cảnh báo | Trả thành công, thông báo hiện, sách thành 'Có sẵn', không cảnh báo | **PASS** | `[images/TC-05-01.png]` | |
| **TC-05-02** | Trả sách | Trả thành công, có cảnh báo quá hạn | Không có dữ liệu quá hạn trên môi trường test, chưa thể tạo data quá hạn | **BLOCKED** | | |
| **TC-05-03** | Trả sách | Hệ thống ẩn nút "Trả sách" trên phiếu đã trả | Không hiển thị nút "Trả sách" trên phiếu đã trả → ngăn chặn được việc bấm lại | **PASS** | `[images/TC-05-03.jpeg]` | |
| **TC-05-04** | Trả sách | Chuyển hướng về trang đăng nhập | Chuyển hướng thành công về trang login | **PASS** | `[images/TC-05-04.png]` | |
| **TC-05-05** | Trả sách | Khi hủy thao tác, trạng thái phiếu không đổi | Khi nhấn 'Trả sách', hệ thống thực hiện trả ngay lập tức, không hiển thị popup xác nhận để chọn Hủy | **FAIL** | `[images/TC-05-05.png]` | `BUG-REQ05-01` |
| **TC-06-01** | Xử lý quá hạn | Tự động cập nhật phiếu (bao gồm BR001) thành "Quá hạn" | Đã quét và cập nhật thành công các phiếu quá hạn (bao gồm phiếu BR001) | **PASS** | `[images/tc-06-01.png]` | |
| **TC-06-02** | Xử lý quá hạn | Thông báo 0 phiếu, không thay đổi | Hệ thống luôn tồn tại sẵn phiếu quá hạn từ trước, không thể làm sạch dữ liệu để test | **BLOCKED** | | |
| **TC-06-03** | Xử lý quá hạn | Bộ lọc chỉ hiển thị duy nhất phiếu quá hạn | Danh sách hiển thị lẫn lộn cả phiếu 'quá hạn' và phiếu 'đã trả' mặc dù đang chọn bộ lọc 'Quá hạn' | **FAIL** | `[images/TC-06-03.jpeg]` | `BUG-REQ06-01` |
| **TC-06-04** | Xử lý quá hạn | Thành viên thấy phiếu quá hạn (màu đỏ/chữ đậm) | Phiếu hiển thị rõ trạng thái 'quá hạn' trên giao diện của Thành viên | **PASS** | `[images/TC-06-04.jpeg]` | |
| **TC-06-05** | Xử lý quá hạn | Thành viên không thấy nút, truy cập trực tiếp bị từ chối | Không thấy nút trên giao diện, cố tình truy cập URL trực tiếp thì hệ thống đá sang trang Login | **PASS** | `[images/TC-06-05.jpeg]` | |

---

## 2. Thống kê tiến độ kiểm thử
* **Tổng số kịch bản thiết kế:** 10 test cases.
* **Số trường hợp Đạt (PASS):** 6 / 10 (60%).
* **Số trường hợp Lỗi (FAIL):** 2 / 10 (20%).
* **Số trường hợp Bị nghẽn (BLOCKED):** 2 / 10 (20%) *(Do hạn chế về việc kiểm soát/làm sạch data trên môi trường chạy thử)*.