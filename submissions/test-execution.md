# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin | |
|---|---|
| **Nhóm** | <!-- Nhóm 3 --> |
| **Ngày thực thi** | 23/5/2026 |
| **Trình duyệt** | Chrome 148.0.7778.178 |
| **Hệ điều hành** | Windows |

---

## Kết quả chi tiết

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|---|---|---|---|---|---|---|
| **TC-13** | REQ-04 — Mượn sách | Mượn thành công, sách đổi trạng thái sang "Borrowed", tạo phiếu mượn mới. | Đúng như mong đợi. Hệ thống hiển thị toast thành công, sách chuyển màu đỏ "Borrowed". | **Pass** | | |
| **TC-14** | REQ-04 — Mượn sách | Chặn mượn sách đối với tài khoản đang bị Tạm ngưng (Blocked). | Đúng như mong đợi. Hệ thống hiển thị dialog báo lỗi tài khoản bị tạm ngưng. | **Pass** | | |
| **TC-15** | REQ-04 — Mượn sách | Chặn mượn sách đối với tài khoản đã Hết hạn (Expired). | Đúng như mong đợi. Hệ thống hiển thị dialog báo lỗi tài khoản đã hết hạn. | **Pass** | | |
| **TC-16** | REQ-04 — Mượn sách | Chặn mượn từ cuốn thứ 4 (Giới hạn tối đa 3 cuốn). | **Lỗi:** Hệ thống không chặn, vẫn cho phép mượn đến cuốn thứ 4, thứ 5 bình thường. | **Fail** | `` | `BUG-01` |
| **TC-17** | REQ-04 — Mượn sách | Vô hiệu hóa nút mượn đối với các cuốn sách đã bị mượn trước đó. | Đúng như mong đợi. Nút mượn sách bị mờ xám (disabled) không cho nhấn. | **Pass** | | |

## Tổng hợp kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | `<!-- số -->` |
| Pass | `<!-- số -->` |
| Fail | `<!-- số -->` |
| Blocked | `<!-- số -->` |
| Not Run | `<!-- số -->` |
| **Tỷ lệ Pass** | `<!-- xx% -->` |

### Kết quả theo nhóm chức năng

| Nhóm | Tổng TC | Pass | Fail | Tỷ lệ Pass |
|------|---------|------|------|------------|
| | | | | |
