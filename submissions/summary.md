# Test Summary — Báo cáo tổng hợp kiểm thử

> Đây là hoạt động Quality Assurance nhằm đánh giá chất lượng tổng thể của hệ thống Quản lý Thư viện dựa trên kết quả kiểm thử, mức độ đáp ứng yêu cầu nghiệp vụ và mức độ ảnh hưởng của các lỗi được phát hiện.

---

## 1. Thông tin nhóm

| Mục                   | Thông tin                  |
| --------------------- | -------------------------- |
| **Nhóm**              | STQA-03                    |
| **Lớp**               | STQA                       |
| **Ngày báo cáo**      | 23/05/2026                 |
| **Hệ thống kiểm thử** | https://stqa.rbc.vn — v1.0 |

---

## 2. Tổng quan kết quả

| Chỉ số               | Giá trị |
| -------------------- | ------- |
| Tổng số test case    | 39      |
| Pass                 | 29      |
| Fail                 | 8       |
| Blocked              | 2       |
| Not Run              | 0       |
| **Tỷ lệ Pass**       | 74.35%  |
| **Số bug phát hiện** | 8       |

### Phân bổ theo nhóm chức năng

| Nhóm chức năng              | TC | Pass | Fail | Bug | Đánh giá      |
| --------------------------- | -- | ---- | ---- | --- | ------------- |
| REQ-01: Đăng nhập           | 5  | 5    | 0    | 0   | Tốt           |
| REQ-02: Xem danh sách sách  | 4  | 3    | 1    | 1   | Khá           |
| REQ-03: Tìm kiếm & Lọc sách | 6  | 4    | 2    | 2   | Cần cải thiện |
| REQ-04: Mượn sách           | 5  | 4    | 1    | 1   | Cần cải thiện |
| REQ-05: Trả sách            | 5  | 3    | 1    | 1   | Trung bình    |
| REQ-06: Xử lý quá hạn       | 5  | 3    | 1    | 1   | Trung bình    |
| REQ-07: Quản lý thành viên  | 4  | 2    | 2    | 2   | Yếu           |
| REQ-08: Tra cứu phiếu mượn  | 5  | 5    | 0    | 0   | Tốt           |

### Phân bổ bug theo mức độ

| Mức độ | Số lượng | Bug IDs                                                |
| ------ | -------- | ------------------------------------------------------ |
| High   | 5        |   BUG-REQ01-01,BUG-REQ03-02,BUG-REQ04-01,BUG-REQ06-01,BUG-REQ07-01   |
| Medium | 3        | BUG-REQ02-01,BUG-REQ03-01,BUG-REQ05-01 |
| Low    | 0        | Không có                                               |

---

## 3. Kỹ thuật thiết kế đã sử dụng

| Kỹ thuật                                | Áp dụng cho REQ nào?           | Số TC sử dụng | Giải thích cách áp dụng                                                                                                                                                        |
| --------------------------------------- | ------------------------------ | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Equivalence Partitioning (EP)**       | REQ-01, REQ-07, REQ-08         | 10            | Phân chia dữ liệu đầu vào thành các lớp hợp lệ và không hợp lệ (email tồn tại/không tồn tại, email đúng/sai định dạng, email trùng/chưa trùng, tài khoản hợp lệ/không hợp lệ). |
| **Boundary Value Analysis (BVA)**       | REQ-01, REQ-04                 | 2             | Kiểm tra các giá trị tại ngưỡng giới hạn như số lượng sách được mượn tối đa là 3 cuốn hoặc trường dữ liệu rỗng.                                                                |
| **Decision Table Testing**              | REQ-04                         | 5             | Kiểm tra các tổ hợp điều kiện nghiệp vụ khi mượn sách: trạng thái thành viên, trạng thái sách và giới hạn số sách đang mượn.                                                   |
| **State Transition Testing**            | REQ-05, REQ-06, REQ-08         | 6             | Kiểm tra sự thay đổi trạng thái của sách và phiếu mượn (Đang mượn → Đã trả → Quá hạn) cũng như trạng thái tài khoản trong các luồng nghiệp vụ.                                 |
| **Role-Based Testing (Authorization)**  | REQ-02, REQ-06, REQ-07, REQ-08 | 8             | Kiểm tra quyền truy cập và chức năng của từng vai trò (Thủ thư và Thành viên), bao gồm hiển thị chức năng và chặn truy cập trái phép.                                          |
| **Negative Testing**                    | REQ-01, REQ-04, REQ-05, REQ-08 | 8             | Kiểm tra phản hồi của hệ thống với dữ liệu không hợp lệ hoặc thao tác không được phép như đăng nhập sai, mượn sách không hợp lệ, truy cập trái quyền.                          |
| **Happy Path Testing**                  | REQ-02, REQ-03, REQ-05, REQ-06 | 9             | Kiểm tra các luồng nghiệp vụ thành công khi người dùng thao tác đúng và dữ liệu đầu vào hợp lệ.                                                                                |
| **UI / UX Testing**                     | REQ-02, REQ-05, REQ-06, REQ-08 | 6             | Kiểm tra hiển thị giao diện, cấu trúc dữ liệu, nút chức năng, trạng thái màu sắc và trải nghiệm người dùng.                                                                    |
| **Filter / Search Testing**             | REQ-03                         | 6             | Kiểm tra chức năng tìm kiếm, lọc dữ liệu, xử lý chuỗi nhập liệu, kết hợp điều kiện tìm kiếm và reset bộ lọc.                                                                   |
| **Real-time / Synchronization Testing** | REQ-02                         | 1             | Kiểm tra khả năng đồng bộ trạng thái dữ liệu giữa nhiều phiên làm việc mà không cần tải lại trang.                                                                             |




## 4. Phân tích chất lượng phần mềm

### 4.1. Điểm mạnh

* Chức năng Đăng nhập (REQ-01) hoạt động ổn định với tỷ lệ Pass 100%.
* Chức năng Tra cứu phiếu mượn (REQ-08) đáp ứng đầy đủ yêu cầu và đạt tỷ lệ Pass 100%.
* Các luồng nghiệp vụ chính như xem sách, mượn sách và trả sách đều có thể thực hiện thành công trong điều kiện bình thường.
* Cơ chế phân quyền giữa Thành viên và Thủ thư được triển khai tương đối chính xác.
* Giao diện hệ thống dễ sử dụng, thông tin hiển thị rõ ràng và nhất quán.

### 4.2. Điểm yếu

* Chức năng Quản lý thành viên (REQ-07) tồn tại lỗi nghiêm trọng trong kiểm tra định dạng email, vừa từ chối email hợp lệ vừa chấp nhận email không hợp lệ.
* Chức năng Tìm kiếm & Lọc sách (REQ-03) xử lý chưa chính xác khi kết hợp nhiều điều kiện tìm kiếm và lọc.
* Chức năng Mượn sách (REQ-04) không giới hạn số lượng sách được phép mượn theo yêu cầu nghiệp vụ.
* Chức năng Trả sách (REQ-05) thiếu bước xác nhận trước khi thực hiện hành động cập nhật dữ liệu.
* Bộ lọc phiếu quá hạn (REQ-06) hiển thị dữ liệu không chính xác.
* Một số trường hợp kiểm thử không thể thực hiện do hạn chế về dữ liệu và môi trường kiểm thử.

---

## 5. Đề xuất ưu tiên sửa lỗi

> Tiêu chí ưu tiên được xác định dựa trên mức độ ảnh hưởng đến nghiệp vụ cốt lõi của hệ thống và mức độ nghiêm trọng của lỗi.

| Thứ tự | Bug          | Mức độ | Lý do ưu tiên                                                                                        |
| ------ | ------------ | ------ | ---------------------------------------------------------------------------------------------------- |
| 1      | BUG-REQ04-01 | High   | Vi phạm quy tắc nghiệp vụ quan trọng khi cho phép mượn vượt quá giới hạn quy định.                   |
| 2      | BUG-02       | High   | Chấp nhận email sai định dạng, làm giảm chất lượng dữ liệu và ảnh hưởng đến các chức năng liên quan. |
| 3      | BUG-01       | High   | Từ chối email hợp lệ, ảnh hưởng trực tiếp đến việc quản lý thành viên.                               |
| 4      | BUG-REQ03-02 | High   | Logic tìm kiếm và lọc hoạt động sai, trả về kết quả không chính xác cho người dùng.                  |
| 5      | BUG-REQ06-01 | Medium | Bộ lọc quá hạn hiển thị sai dữ liệu, ảnh hưởng đến khả năng quản lý phiếu mượn.                      |
| 6      | BUG-REQ03-01 | Medium | Không xử lý khoảng trắng dư thừa trong từ khóa tìm kiếm.                                             |
| 7      | BUG-REQ05-01 | Medium | Thiếu cơ chế xác nhận trước khi trả sách, dễ gây thao tác nhầm.                                      |
| 8      | BUG-REQ02-01 | Medium | Trạng thái sách không đồng bộ tức thời giữa các phiên làm việc.                                      |

---

## 6. Kết luận

Qua quá trình thực hiện 39 test case, hệ thống đạt tỷ lệ Pass 74.35%, phát hiện tổng cộng 8 lỗi và có 2 trường hợp Blocked do thiếu dữ liệu kiểm thử.

Kết quả cho thấy các chức năng cơ bản của hệ thống đã hoạt động tương đối ổn định, đặc biệt là chức năng Đăng nhập và Tra cứu phiếu mượn. Tuy nhiên, hệ thống vẫn tồn tại nhiều lỗi ảnh hưởng trực tiếp đến nghiệp vụ chính như giới hạn mượn sách, quản lý thành viên và xử lý tìm kiếm dữ liệu.

Với các lỗi mức High hiện tại, nhóm đánh giá hệ thống chưa đáp ứng điều kiện phát hành chính thức. Cần ưu tiên khắc phục các lỗi nghiêm trọng, thực hiện kiểm thử hồi quy và xác nhận lại toàn bộ các chức năng liên quan trước khi triển khai lên môi trường Production.

---

## 7. Bài học rút ra

* Việc xây dựng Input Domain Model (IDM) trước khi thiết kế Test Case giúp xác định đầy đủ các lớp dữ liệu cần kiểm thử.
* Các lỗi nghiêm trọng thường tập trung ở phần xử lý nghiệp vụ hơn là giao diện người dùng.
* Chất lượng dữ liệu kiểm thử ảnh hưởng trực tiếp đến khả năng thực hiện đầy đủ các kịch bản kiểm thử.
* Việc duy trì mối liên kết giữa Requirement, Test Case, Test Execution và Bug Report giúp nâng cao khả năng truy vết và quản lý chất lượng.

---

## 8. Khai báo sử dụng AI

| Công cụ AI | Dùng cho phần nào                                                    | Bạn đã kiểm tra/chỉnh sửa thế nào                                              |
| ---------- | -------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| ChatGPT    | Hỗ trợ rà soát Test Case, Bug Report và xây dựng Test Summary Report | Nhóm đã kiểm tra, chỉnh sửa và xác nhận lại toàn bộ nội dung trước khi sử dụng |
