# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin         |                                    |
| ----------------- | ---------------------------------- |
| **Nhóm**          | `<!-- Tên nhóm -->`                |
| **Ngày thực thi** | `<!-- DD/MM/YYYY -->`              |
| **Trình duyệt**   | Chrome `<!-- version -->`          |
| **Hệ điều hành**  | `<!-- Windows / macOS / Linux -->` |

---

## Kết quả chi tiết

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
| ----- | -------------- | -------------------------- | --------------- | -------- | ---------- | --- |
|       |                |                            |                 |          |            |     |

---

## Tổng hợp kết quả

| Chỉ số            | Giá trị        |
| ----------------- | -------------- |
| Tổng số test case | `<!-- số -->`  |
| Pass              | `<!-- số -->`  |
| Fail              | `<!-- số -->`  |
| Blocked           | `<!-- số -->`  |
| Not Run           | `<!-- số -->`  |
| **Tỷ lệ Pass**    | `<!-- xx% -->` |

### Kết quả theo nhóm chức năng

| Nhóm | Tổng TC | Pass | Fail | Tỷ lệ Pass |
| ---- | ------- | ---- | ---- | ---------- |
|      |         |      |      |            |

# Test Execution — Kết quả thực thi kiểm thử (Thành viên E - REQ-08)

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin         |                                 |
| ----------------- | ------------------------------- |
| **Nhóm**          | `Nhóm 3`                        |
| **Ngày thực thi** | `22/05/2026`                    |
| **Trình duyệt**   | Chrome `Version 125.0.6422.112` |
| **Hệ điều hành**  | `Windows / macOS`               |

---

## Kết quả chi tiết

| Mã TC           | Nhóm chức năng             | Kết quả mong đợi (tóm tắt)                                                                                                                                            | Kết quả thực tế                                                                                                                                                        | Kết luận | Minh chứng                             | Bug      |
| --------------- | -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------------------------------------- | -------- |
| **TC-REQ08-01** | REQ-08: Tra cứu phiếu mượn | Đăng nhập tài khoản Thành viên (dam.tran@email.com), hệ thống chỉ hiển thị đúng 2 phiếu mượn cá nhân (BR002, BR005).                                                  | Đăng nhập thành công tài khoản Trần Dựa Dẫm. Giao diện hiển thị đúng và chỉ xuất hiện duy nhất 2 phiếu mượn BR002 và BR005.                                            | **Pass** | `docs/assets/evidence-tc-req08-01.png` | Không có |
| **TC-REQ08-02** | REQ-08: Tra cứu phiếu mượn | Đăng nhập tài khoản Thủ thư, hiển thị đủ 5 phiếu. Nhấn nút quét quá hạn, phiếu BR001 và BR003 đổi sang màu đỏ "Quá hạn", SnackBar hiện thông báo cập nhật thành công. | Hệ thống hiển thị đủ cả 5 phiếu mượn của mọi thành viên. Sau khi bấm nút, trạng thái BR001 và BR003 chuyển đỏ, SnackBar hiển thị: "Đã cập nhật: 2 phiếu mượn quá hạn." | **Pass** | `docs/assets/evidence-tc-req08-02.png` | Không có |
| **TC-REQ08-03** | REQ-08: Tra cứu phiếu mượn | Khối thông tin của phiếu (ví dụ BR003) hiển thị đầy đủ 5 trường thông tin, phông chữ ngay ngắn không chồng chéo, nhãn trạng thái trực quan.                           | Khối thông tin hiển thị rõ ràng, không bị lỗi font hay đè chữ. Đầy đủ mã phiếu, tên sách, tên người mượn, cặp ngày và nhãn trạng thái trực quan.                       | **Pass** | `docs/assets/evidence-tc-req08-03.png` | Không có |
| **TC-REQ08-04** | REQ-08: Tra cứu phiếu mượn | Đăng nhập sai thông tin, hệ thống từ chối truy cập và chặn hoàn toàn không cho tiếp cận phân hệ tra cứu phiếu mượn.                                                   | Hệ thống báo lỗi đăng nhập, giữ nguyên màn hình đăng nhập và không để lộ dữ liệu tra cứu phiếu mượn.                                                                   | **Pass** | `docs/assets/evidence-tc-req08-04.png` | Không có |
| **TC-REQ08-05** | REQ-08: Tra cứu phiếu mượn | Đăng nhập tài khoản có trạng thái Tạm ngưng/Hết hạn nhưng không có phiếu nào, màn hình hiển thị thông báo trống: "Chưa có phiếu mượn nào."                            | Giao diện không hiện phiếu của người khác, hiển thị màn hình trống kèm dòng chữ thông báo chính xác: "Chưa có phiếu mượn nào."                                         | **Pass** | `docs/assets/evidence-tc-req08-05.png` | Không có |

---

## Tổng hợp kết quả

| Chỉ số            | Giá trị |
| ----------------- | ------- |
| Tổng số test case | `5`     |
| Pass              | `5`     |
| Fail              | `0`     |
| Blocked           | `0`     |
| Not Run           | `0`     |
| **Tỷ lệ Pass**    | `100%`  |

### Kết quả theo nhóm chức năng

| Nhóm                       | Tổng TC | Pass | Fail | Tỷ lệ Pass |
| -------------------------- | ------- | ---- | ---- | ---------- |
| REQ-08: Tra cứu phiếu mượn | 5       | 5    | 0    | 100%       |
