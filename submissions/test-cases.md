# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Viết tối thiểu **20 TC** phủ đủ các chức năng chính (REQ-01 → REQ-08).
> Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.
> Tự tổ chức và phân nhóm test case theo cách hợp lý nhất.

| Thông tin      |                       |
| -------------- | --------------------- |
| **Nhóm**       | `<!-- Tên nhóm -->`   |
| **Ngày tạo**   | `<!-- DD/MM/YYYY -->` |
| **Hệ thống**   | https://stqa.rbc.vn   |
| **Tham chiếu** | SRS v1.0              |

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

> 📖 **Textbook:** Chương 6 — _Input Domain Modeling_, Paul Ammann & Jeff Offutt.
>
> **Trước khi viết Test Case**, nhóm **phải** phân tích miền đầu vào bằng bảng IDM bên dưới.
> Mỗi chức năng cần xác định: **Đặc tính (Characteristic)**, **Phân vùng (Block/Partition)**, và **Giá trị đại diện (Value)**.

### IDM — Đăng nhập (REQ-01)

| Đặc tính (Characteristic)  | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi             |
| -------------------------- | ----------------- | ------------------------ | ---------------------------- |
| Email có tồn tại trong DB? | Có                | `librarian@library.com`  | Đăng nhập thành công         |
|                            | Không             | `noone@email.com`        | Thông báo lỗi                |
| Mật khẩu có đúng?          | Đúng              | `admin123`               | Đăng nhập thành công         |
|                            | Sai               | `wrongpass`              | Thông báo lỗi                |
| Ô nhập có rỗng?            | Không rỗng        | (giá trị bất kỳ)         | Xử lý bình thường            |
|                            | Rỗng              | `""`                     | Thông báo "Vui lòng nhập..." |

### IDM — Tìm kiếm sách (REQ-03)

| Đặc tính (Characteristic)    | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi                 |
| ---------------------------- | ----------------- | ------------------------ | -------------------------------- |
| Từ khóa có tồn tại trong DB? | Có (tên sách)     | `"Flutter"`              | Hiển thị sách chứa "Flutter"     |
|                              | Có (tên tác giả)  | `"Nguyễn"`               | Hiển thị sách của tác giả Nguyễn |
|                              | Không             | `"XYZ123"`               | Danh sách rỗng                   |
| Phân biệt HOA/thường?        | Chữ thường        | `"flutter"`              | Kết quả giống "Flutter"          |
|                              | Chữ HOA           | `"FLUTTER"`              | Kết quả giống "Flutter"          |

### IDM — Mượn sách (REQ-04, REQ-05)

| Đặc tính (Characteristic) | Phân vùng (Block)   | Giá trị đại diện (Value) | Kết quả mong đợi                 |
| ------------------------- | ------------------- | ------------------------ | -------------------------------- |
| Trạng thái sách?          | Có sẵn              | BOOK001                  | Cho phép mượn                    |
|                           | Đang mượn           | BOOK003                  | Không cho phép                   |
|                           | Thất lạc            | BOOK007                  | Không cho phép                   |
| Trạng thái thành viên?    | Hoạt động           | MEM002                   | Cho phép mượn                    |
|                           | Tạm ngưng           | MEM004                   | Từ chối, thông báo lỗi           |
|                           | Hết hạn             | MEM005                   | Từ chối, thông báo lỗi           |
| Số sách đang mượn?        | < 3 (BVA: 0, 1, 2)  | MEM006 (0 sách)          | Cho phép mượn                    |
|                           | = 3 (BVA: giới hạn) | MEM đã mượn 3 sách       | Từ chối, thông báo vượt giới hạn |

### IDM — `<!-- Nhóm tự bổ sung cho REQ-05 đến REQ-08 -->`

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
| ------------------------- | ----------------- | ------------------------ | ---------------- |
| `<!-- Nhóm tự điền -->`   |                   |                          |                  |

> 💡 **Gợi ý kỹ thuật**: Sử dụng **Phân lớp tương đương (EP)** cho các phân vùng rời rạc, **Phân tích giá trị biên (BVA)** cho các phân vùng số (ví dụ: giới hạn 3 sách). Xem textbook §6.1–6.3.

---

## Bước 2: Test Cases

<!-- Tự tổ chức bảng test case: có thể chia nhóm theo chức năng, theo REQ, hoặc theo luồng nghiệp vụ — tùy nhóm quyết định. -->
<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
| ----- | ----------------- | -------------- | -------------- | --------------- | ---------------- | --- | -------- |
|       |                   |                |                |                 |                  |     |          |

---

## Tổng hợp

| Nhóm chức năng | Số TC             | REQ phủ | Kỹ thuật IDM áp dụng |
| -------------- | ----------------- | ------- | -------------------- |
|                |                   |         |                      |
| **Tổng**       | **<!-- ≥ 20 -->** |         |                      |

## REQ-08: Kiểm thử chức năng Tra cứu phiếu mượn (Thành viên E thực hiện)

| Mã TC           | Mục tiêu kiểm thử                                                                                        | Tiền điều kiện                                                                                                      | Bước thực hiện                                                                                                                                                                                                                                                                                                                    | Dữ liệu đầu vào                                                                                                                     | Kết quả mong đợi (Strong Oracle)                                                                                                                                                                                                                                                                      | REQ    | Kỹ thuật                                          |
| :-------------- | :------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----- | :------------------------------------------------ |
| **TC-REQ08-01** | Quyền bảo mật tra cứu danh sách phiếu mượn của tài khoản Thành viên                                      | Trình duyệt đã được làm mới (F5) để khôi phục dữ liệu gốc. Người dùng đang ở trang đăng nhập.                       | 1. Nhập Email thành viên hợp lệ vào ô Email.<br>2. Nhập Mật khẩu hợp lệ vào ô Mật khẩu.<br>3. Nhấn nút **Đăng nhập**.<br>4. Điều hướng đến tab **"Phiếu mượn của tôi"**.<br>5. Quan sát danh sách các phiếu mượn hiển thị.                                                                                                        | Email: `dam.tran@email.com`<br>Mật khẩu: `password123`<br>(Tài khoản Trần Dựa Dẫm)                                                  | Đăng nhập thành công, hiển thị đúng tên "Trần Dựa Dẫm (Thành viên)". Hệ thống chỉ hiển thị duy nhất danh sách 2 phiếu mượn thuộc sở hữu của tài khoản này (BR002 và BR005). Tuyệt đối không hiển thị phiếu mượn của thành viên khác.                                                                  | REQ-08 | EP (Phân lớp tương đương)                         |
| **TC-REQ08-02** | Quyền tra cứu dữ liệu tổng hợp và kích hoạt cập nhật phiếu quá hạn của Thủ thư                           | Trình duyệt đã được làm mới (F5) để khôi phục dữ liệu gốc về trạng thái ban đầu. Người dùng đang ở trang đăng nhập. | 1. Nhập Email của Thủ thư vào ô Email.<br>2. Nhập Mật khẩu của Thủ thư vào ô Mật khẩu.<br>3. Nhấn nút **Đăng nhập**.<br>4. Điều hướng đến tab **"Mượn / Trả"**.<br>5. Nhấn vào nút **"Kiểm tra sách quá hạn"** ở thanh công cụ phía trên.<br>6. Quan sát sự thay đổi trạng thái và nội dung thanh thông báo (SnackBar) phía dưới. | Email: `librarian@library.com`<br>Mật khẩu: `admin123`<br>(Tài khoản Thủ thư)                                                       | Đăng nhập thành công, hiển thị đúng tên "Nguyễn Thủ Thư (Thủ thư)". Hệ thống hiển thị toàn bộ 5 phiếu mượn. Sau khi nhấn nút, trạng thái phiếu BR001 và BR003 chuyển sang màu đỏ "Quá hạn", đồng thời thanh thông báo hiển thị đúng: "Đã cập nhật: 2 phiếu mượn quá hạn."                             | REQ-08 | Kịch bản luồng chức năng (Functional Flow)        |
| **TC-REQ08-03** | Kiểm tra cấu trúc hiển thị thông tin chi tiết trên mỗi khối Phiếu mượn                                   | Người dùng đang đăng nhập bằng tài khoản Thủ thư hoặc Thành viên và đang đứng ở màn hình danh sách phiếu mượn.      | 1. Giữ nguyên màn hình ở tab **"Mượn / Trả"**.<br>2. Chọn một phiếu bất kỳ trong danh sách (Ví dụ: chọn phiếu **BR003** - sách _Quản trị nhân sự hiện đại_).<br>3. Soi kỹ các thành phần thông tin hiển thị trên khối dữ liệu của hàng đó.                                                                                        | Đối tượng kiểm tra: Khối thông tin của phiếu mượn mã **BR003** trên giao diện.                                                      | Khối phiếu mượn bắt buộc phải hiển thị đầy đủ 5 nhóm thông tin cấu trúc, phông chữ ngay ngắn không bị đè chữ: <br>1. Mã phiếu (BR003)<br>2. Sách mượn (Quản trị nhân sự hiện đại)<br>3. Tên thành viên (Hoàng Cá Biệt)<br>4. Cặp ngày (Ngày mượn và Hạn trả)<br>5. Nhãn trạng thái màu sắc trực quan. | REQ-08 | Kiểm thử cấu trúc giao diện (UI Testing)          |
| **TC-REQ08-04** | Kiểm tra chặn quyền tra cứu phiếu mượn khi đăng nhập bằng dữ liệu không hợp lệ (Negative Test)           | Trình duyệt đã được làm mới (F5). Người dùng đang ở màn hình đăng nhập.                                             | 1. Nhập Email không tồn tại hoặc sai mật khẩu vào ô nhập liệu.<br>2. Nhấn nút **Đăng nhập**.<br>3. Quan sát phản hồi của hệ thống.                                                                                                                                                                                                | **Trường hợp 1:** Email: `ba.nguyen@email.com` / MK: `wrongpassword`<br>**Trường hợp 2:** Email: `nobody@test.com` / MK: `anything` | Hệ thống từ chối quyền truy cập, hiển thị thông báo lỗi đăng nhập rõ ràng. Giao diện không chuyển hướng vào bên trong và chặn hoàn toàn không cho tiếp cận phân hệ tra cứu phiếu mượn.                                                                                                                | REQ-08 | Kiểm thử kịch bản lỗi (Negative Testing)          |
| **TC-REQ08-05** | Kiểm tra quyền bảo mật tra cứu của các tài khoản Thành viên có trạng thái đặc biệt (Tạm ngưng / Hết hạn) | Trình duyệt đã được làm mới (F5) để khôi phục dữ liệu gốc. Người dùng đang ở màn hình đăng nhập.                    | 1. Thực hiện đăng nhập lần lượt với từng tài khoản có trạng thái đặc biệt.<br>2. Di chuyển đến tab **"Phiếu mượn của tôi"**.<br>3. Quan sát danh sách hiển thị và thông báo ở giữa màn hình.                                                                                                                                      | **Tài khoản 1 (Tạm ngưng):** `cu.le@email.com`<br>**Tài khoản 2 (Hết hạn):** `binh.pham@email.com`                                  | Hệ thống đảm bảo an toàn thông tin phân quyền: Vì cả hai tài khoản này không sở hữu phiếu nào trong dữ liệu gốc, giao diện bắt buộc không được hiển thị phiếu của người khác và phải xuất hiện thông báo trống rõ ràng: "Chưa có phiếu mượn nào."                                                     | REQ-08 | Kiểm thử trạng thái dữ liệu (State-Based Testing) |
