# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

| Thông tin | |
|---|---|
| **Nhóm** | `<!-- Tên nhóm -->` |
| **Ngày báo cáo** | `<!-- DD/MM/YYYY -->` |

---

## Danh sách báo cáo lỗi (Bug Reports) - REQ-04

### BUG-01: Thành viên có thể mượn sách vượt quá giới hạn cho phép (Tối đa 3 cuốn)

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-01 |
| **TC liên quan** | `TC-16` |
| **REQ liên quan** | `REQ-04` — Mượn sách |
| **Mức độ** | High / Critical |
| **Người phát hiện** | `` |
| **Ngày phát hiện** | 23/05/2026 |
| **Trạng thái** | Open |

**Tiêu đề:**
Hệ thống không chặn hành động mượn sách khi tài khoản thành viên hoạt động đã mượn vượt quá số lượng giới hạn tối đa cho phép (3 cuốn).

**Môi trường:**
- Trình duyệt: Chrome (Phiên bản mới nhất)
- Hệ điều hành: Windows / macOS / Linux ``
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**
Hệ thống ở trạng thái dữ liệu gốc ban đầu (sau khi reset hoặc vừa tải lại trang), tài khoản thành viên đang ở trạng thái hoạt động (Active).

**Bước tái hiện:**
1. Truy cập hệ thống https://stqa.rbc.vn và đăng nhập bằng tài khoản `dam.tran@email.com` / `password123`.
2. Truy cập danh sách sách, tiến hành nhấn nút "Mượn sách" (Borrow) lần lượt cho 3 cuốn sách bất kỳ đang ở trạng thái "Sẵn sàng" (Ví dụ: BOOK001, BOOK002, BOOK003).
3. Tìm tiếp cuốn sách thứ 4 đang ở trạng thái "Sẵn sàng" (Ví dụ: BOOK004) và tiếp tục nhấn nút "Mượn sách".

**Kết quả mong đợi:**
Hệ thống phải chặn hành động mượn sách ở cuốn thứ 4 (bước 3), không cho phép tạo thêm phiếu mượn và hiển thị thông báo lỗi rõ ràng trên giao diện: "Đã đạt giới hạn mượn tối đa (3 cuốn)".

**Kết quả thực tế:**
Hệ thống vẫn cho phép mượn thành công cuốn sách thứ 4 (và các cuốn tiếp theo). Cuốn sách đổi trạng thái sang "Đã mượn" bình thường và không xuất hiện bất kỳ thông báo lỗi chặn giới hạn nào.

**Tác động:**
Vi phạm quy tắc nghiệp vụ cốt lõi của thư viện được mô tả trong tài liệu đặc tả SRS (§3.1), gây thất thoát sách và sai lệch logic quản lý số lượng mượn trả.

**Minh chứng:**
`TÍ CHÈN ẢNH`

**Đề xuất xử lý:**
Bổ sung một hàm kiểm tra (Validation check) ở phía Backend và Frontend tại thời điểm người dùng nhấn nút "Mượn sách": Đếm tổng số lượng phiếu mượn chưa trả của User ID hiện tại, nếu kết quả $\ge 3$ thì lập tức trả về lỗi và vô hiệu hóa nút bấm.

## BUG-02

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-02 |
| **TC liên quan** | `<!-- TC-xx -->` |
| **REQ liên quan** | `<!-- REQ-xx -->` |
| **Mức độ** | `<!-- High / Medium / Low -->` |
| **Người phát hiện** | `<!-- Họ tên thành viên -->` |
| **Ngày phát hiện** | `<!-- DD/MM/YYYY -->` |
| **Trạng thái** | `<!-- Open / Closed -->` |

**Tiêu đề:**
`<!-- Mô tả hành vi lỗi -->`

**Bước tái hiện:**
1. `<!-- -->`
2. `<!-- -->`
3. `<!-- -->`

**Kết quả mong đợi:**
`<!-- -->`

**Kết quả thực tế:**
`<!-- -->`

**Tác động:**
`<!-- -->`

**Minh chứng:**
`<!-- -->`

**Đề xuất xử lý:**
`<!-- -->`

---

<!-- Copy template BUG trên để thêm BUG-03, BUG-04, ... cho mỗi TC Fail -->
