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

## Danh sách báo cáo lỗi (Bug Reports) - REQ-04

### BUG-01: Thành viên có thể mượn sách vượt quá giới hạn cho phép (Tối đa 3 cuốn)

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-01 |
| **TC liên quan** | `TC-16` |
| **REQ liên quan** | `REQ-04` — Mượn sách |
| **Mức độ** | High / Critical |
| **Người phát hiện** | Nguyễn Hoàng Anh |
| **Ngày phát hiện** | 24/05/2026 |
| **Trạng thái** | Open |

**Tiêu đề:**
Hệ thống không giới hạn số lượng sách mượn tối đa của thành viên, cho phép mượn cuốn thứ 4 và thứ 5 mà không có thông báo chặn lỗi.

**Môi trường:**
- Trình duyệt: Chrome (Phiên bản mới nhất)
- Hệ điều hành: Windows 11
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**
Hệ thống ở trạng thái dữ liệu gốc, tài khoản thành viên đang ở trạng thái hoạt động bình thường (Active).

**Bước tái hiện:**
1. Truy cập hệ thống https://stqa.rbc.vn và tiến hành đăng nhập bằng tài khoản `dam.tran@email.com` / `password123`.
2. Tại màn hình danh sách sách, lần lượt nhấn nút "Mượn sách" (Borrow) cho 3 cuốn sách bất kỳ đang "Sẵn sàng" (Ví dụ: BOOK001, BOOK002, BOOK003).
3. Tiếp tục tìm cuốn sách thứ 4 đang ở trạng thái "Sẵn sàng" (Ví dụ: BOOK004) và nhấn nút "Mượn sách".

**Kết quả mong đợi:**
Hệ thống phải kiểm tra số lượng sách đang mượn, chặn hành động mượn cuốn thứ 4 và hiển thị thông báo lỗi rõ ràng trên giao diện theo đặc tả SRS §3.1: "Đã đạt giới hạn mượn tối đa (3 cuốn)".

**Kết quả thực tế:**
Hệ thống không chặn, vẫn cho phép tạo phiếu mượn thành công cho cuốn thứ 4 (và tiếp tục cho phép mượn thêm nhiều cuốn khác). Sách đổi trạng thái sang "Đã mượn" bình thường.

**Tác động:**
Vi phạm nghiêm trọng quy tắc nghiệp vụ (Business Rule) cốt lõi của thư viện được mô tả trong tài liệu SRS, dẫn đến việc quản lý thất thoát sách và sai lệch số liệu.

**Minh chứng:**
``

**Đề xuất xử lý:**
Bổ sung một hàm kiểm tra logic (Validation) trước khi xử lý mượn: Đếm số phiếu mượn có trạng thái chưa trả của UserID hiện tại, nếu kết quả $\ge 3$ thì chặn hành động và trả về thông báo lỗi ở cả Frontend và Backend.

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
