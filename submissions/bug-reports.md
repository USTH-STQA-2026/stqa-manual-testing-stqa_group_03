# Danh sách Báo cáo lỗi (Bug Reports) - Phân hệ Quản lý thành viên (REQ-07)

| Thông tin      |                          |
| -------------- | ------------------------ |
| **Nhóm**       | `<!-- STQA_Group_03 -->` |
| **Ngày tạo**   | `<!-- 19/05/2026 -->`    |
| **Hệ thống**   | https://stqa.rbc.vn      |
| **Tham chiếu** | SRS v1.0                 |

---

## 1. BUG-REQ01-01: Chặn nhầm email hợp lệ

**Bug ID:** BUG-01 (Tham chiếu: TC-REQ07-01)

**Tiêu đề:** Hệ thống báo lỗi "Email không hợp lệ" và từ chối thêm mới khi nhập email hoàn toàn đúng định dạng (VD: binh.ly@email.com)

**Môi trường:**

- Trình duyệt: Chrome Version 125.0.0
- Hệ điều hành: Windows / macOS
- Ứng dụng: Hệ thống Mượn sách thư viện (https://stqa.rbc.vn)

**Điều kiện tiên quyết:**

- Người dùng đã đăng nhập thành công bằng tài khoản **Thủ thư** (`librarian@library.com`).
- Đang truy cập ở màn hình **Thêm thành viên mới**.

**Bước tái hiện:**

1. Tại ô **Họ và tên**, nhập: `Lý Tân Binh`.
2. Tại ô **Email**, nhập email hợp lệ có chứa dấu chấm trước @: `binh.ly@email.com`.
3. Tại ô **Số điện thoại**, nhập: `0988111222`.
4. Nhấn nút **Thêm thành viên** màu xanh ở dưới cùng.

**Kết quả mong đợi:**
Hệ thống chấp nhận dữ liệu (do email đã thỏa mãn quy tắc có `@` và có dấu `.` trong domain theo SRS), tiến hành thêm mới thành viên và hiển thị thông báo thêm thành công.

**Kết quả thực tế:**
Hệ thống không lưu dữ liệu, xuất hiện khung cảnh báo màu đỏ với dòng chữ `"Email không hợp lệ."` ngay phía trên nút Thêm thành viên.

**Tác động:**
Nghiệp vụ thêm mới thành viên bị chặn một cách sai lệch đối với những người dùng có địa chỉ email hợp lệ phổ biến (định dạng `[tên].[họ]@domain.com`). Gây bức xúc và gián đoạn công việc của Thủ thư.

**Mức độ:**
**Cao (High)** — Lỗi logic (Validation Logic) làm hỏng luồng chức năng chính của việc Quản lý thành viên. Ngăn cản trực tiếp việc nhập liệu hợp lệ vào hệ thống.

**Minh chứng:**

- Ảnh chụp màn hình đính kèm: <img width="2880" height="1704" alt="image" src="https://github.com/user-attachments/assets/a02adc22-5e26-4691-94ea-6b4fed411f35" />_(Hiển thị form nhập liệu và thông báo lỗi đỏ)_.

**Đề xuất xử lý:**
Kiểm tra lại hàm kiểm tra định dạng email (Regex Validation) ở mã nguồn Frontend và Backend. Cần cập nhật Regex để cho phép ký tự dấu chấm (`.`) nằm ở phần Tên người dùng (Local part - trước dấu `@`).

---

## 2. BUG-REQ02-01: Trạng thái mượn sách không tự động cập nhật theo thời gian thực

**Bug ID:** BUG-02 (Tham chiếu: TC-02-04)

**Tiêu đề:** Hệ thống không tự động cập nhật trạng thái sách theo thời gian thực (Real-time) giữa các phiên làm việc của người dùng khác nhau khi có hành động mượn sách

**Môi trường:**

- Trình duyệt: Chrome Version 125.0.0
- Hệ điều hành: Windows / macOS
- Ứng dụng: Hệ thống Mượn sách thư viện (https://stqa.rbc.vn)

**Điều kiện tiên quyết:**

- Có 2 tài khoản hợp lệ trên hệ thống: một tài khoản Thủ thư và một tài khoản Thành viên.
- Cuốn sách mã số `BOOK001` đang ở trạng thái ban đầu là "Có sẵn".

**Bước tái hiện:**

1. Đăng nhập hệ thống đồng thời trên 2 thiết bị/trình duyệt khác nhau: Phiên 1 sử dụng tài khoản Thủ thư (`librarian@library.com`), Phiên 2 sử dụng tài khoản Thành viên (`dam.tran@email.com`).
2. Tại cả 2 phiên làm việc, cùng điều hướng đến trang chủ và tìm đến cuốn sách `BOOK001` (Quan sát thấy nhãn trạng thái hiển thị đều là "Có sẵn").
3. Tại Phiên 2 (Thành viên), thực hiện nhấn nút mượn cuốn sách `BOOK001` này.
4. Quay trở lại màn hình hiển thị của Phiên 1 (Thủ thư) và quan sát sự thay đổi trạng thái của cuốn sách `BOOK001` mà không thực hiện hành động tải lại trang (F5).

**Kết quả mong đợi:**
Hệ thống phải tự động đồng bộ dữ liệu tức thì theo thời gian thực (Real-time). Trạng thái của cuốn sách `BOOK001` trên màn hình làm việc của Thủ thư phải lập tức tự chuyển sang màu cam "Đang mượn" mà người dùng không cần tải lại trang thủ công.

**Kết quả thực tế:**
Hệ thống không tự động cập nhật trạng thái dữ liệu giữa các phiên. Trên màn hình hiển thị của Thủ thư, cuốn sách `BOOK001` vẫn giữ nguyên nhãn trạng thái cũ là "Có sẵn", chỉ khi nhấn F5 làm mới trình duyệt thì trạng thái mới được cập nhật.

**Tác động:**
Dữ liệu hiển thị bị sai lệch và không đồng bộ giữa các người dùng đang cùng thao tác tại một thời điểm. Điều này có thể dẫn đến việc nhiều Thành viên khác cùng bấm mượn một cuốn sách đã hết, gây xung đột dữ liệu (Race condition) và làm giảm trải nghiệm UI/UX.

**Mức độ:**
**Trung bình (Medium)** — Lỗi logic về đồng bộ hóa dữ liệu thời gian thực (Real-time Synchronization). Chức năng cốt lõi của hệ thống vẫn hoạt động được sau khi F5 nhưng làm ảnh hưởng nghiêm trọng đến tính chính xác trực quan của giao diện.

**Minh chứng:**

- Ảnh chụp màn hình đính kèm: `evidence/bug_10.png` _(Hiển thị hai màn hình song song: một bên đã mượn thành công, một bên vẫn hiện "Có sẵn")_.

**Đề xuất xử lý:**
Tích hợp và cấu hình lại cơ chế kết nối thời gian thực bằng cách sử dụng WebSockets (ví dụ: Socket.io) hoặc cơ chế lắng nghe sự thay đổi dữ liệu liên tục (Real-time listeners/Subscription) ở cả Frontend và Backend để tự động đẩy sự kiện (Emit event) cập nhật trạng thái sách tới tất cả các phiên làm việc đang hoạt động.

---
## BUG-REQ03-01: Hệ thống xử lý sai truy vấn khi từ khóa chứa khoảng trắng ở đầu hoặc cuối (Thiếu logic Trim Space)

**Bug ID:** BUG-03 (Tham chiếu: TC-03-03)

**Tiêu đề:** Hệ thống không chuẩn hóa chuỗi đầu vào (Trim Space) trước khi thực hiện tìm kiếm, dẫn đến trả về kết quả không chính xác

**Môi trường:**

* Trình duyệt: Chrome Version 125.0.0
* Hệ điều hành: Windows / macOS
* Ứng dụng: Hệ thống Mượn sách thư viện (https://stqa.rbc.vn)

**Điều kiện tiên quyết:**

* Người dùng đã đăng nhập bằng tài khoản Thành viên hợp lệ.
* Hệ thống có tồn tại sách với tên **"Lập trình Flutter cơ bản"**.
* Thanh tìm kiếm hoạt động bình thường đối với các từ khóa hợp lệ.

**Bước tái hiện:**

1. Đăng nhập vào hệ thống bằng tài khoản Thành viên hợp lệ.
2. Truy cập trang chủ hệ thống.
3. Tại ô tìm kiếm sách, nhập từ khóa có chứa khoảng trắng ở đầu và cuối: `" Flutter "` (bao gồm một dấu cách trước và sau từ Flutter).
4. Nhấn phím **Enter** hoặc biểu tượng **Tìm kiếm** để thực hiện truy vấn.

**Kết quả mong đợi:**

Hệ thống phải tự động loại bỏ (trim) các khoảng trắng dư thừa ở đầu và cuối chuỗi đầu vào trước khi thực hiện tìm kiếm. Sau khi chuẩn hóa từ khóa thành `"Flutter"`, hệ thống phải trả về kết quả phù hợp là cuốn sách **"Lập trình Flutter cơ bản"**.

**Kết quả thực tế:**

Hệ thống không xử lý loại bỏ khoảng trắng thừa trong chuỗi tìm kiếm. Thay vì thực hiện truy vấn chính xác hoặc thông báo không tìm thấy dữ liệu, hệ thống hiển thị lại toàn bộ danh sách sách mặc định trong thư viện, bao gồm các đầu sách không liên quan như **"Cấu trúc dữ liệu"**, **"Mạng máy tính"**,...

**Tác động:**

* Trả về kết quả tìm kiếm không chính xác, gây nhầm lẫn cho người dùng.
* Làm giảm trải nghiệm sử dụng chức năng tìm kiếm.
* Thể hiện việc xử lý dữ liệu đầu vào chưa đầy đủ và thiếu cơ chế chuẩn hóa dữ liệu trước khi truy vấn.
* Có thể ảnh hưởng đến độ tin cậy của hệ thống khi người dùng nhập dữ liệu với các định dạng khác nhau.

**Mức độ:**

**Trung bình (Medium)** — Lỗi xử lý dữ liệu đầu vào (Input Validation/Input Handling). Không gây mất dữ liệu nhưng ảnh hưởng trực tiếp đến tính chính xác của chức năng tìm kiếm.

**Minh chứng:**

* Ảnh chụp màn hình đính kèm: `<img width="3840" height="2256" alt="image" src="https://github.com/user-attachments/assets/8f657417-80d3-4532-a058-3c198600b08a" />* Quan sát thấy sau khi tìm kiếm với từ khóa `" Flutter "`, hệ thống hiển thị lại toàn bộ danh sách sách thay vì kết quả liên quan đến Flutter.

**Đề xuất xử lý:**

* Thực hiện chuẩn hóa dữ liệu đầu vào bằng hàm `trim()` ở phía Frontend trước khi gửi request tìm kiếm.
* Đồng thời áp dụng xử lý `trim()` ở Backend để đảm bảo tính nhất quán và tránh phụ thuộc hoàn toàn vào Frontend.
* Bổ sung các test case kiểm tra các trường hợp:

  * Khoảng trắng ở đầu chuỗi.
  * Khoảng trắng ở cuối chuỗi.
  * Khoảng trắng ở cả hai đầu chuỗi.
  * Chuỗi chỉ chứa khoảng trắng.
* Đảm bảo truy vấn tìm kiếm luôn được thực hiện trên dữ liệu đã được chuẩn hóa.

---

## 4. BUG-REQ03-02: Ô tìm kiếm ghi đè và bỏ qua hoàn toàn điều kiện lọc của Thể loại sách

**Bug ID:** BUG-04 (Tham chiếu: TC-03-04)

**Tiêu đề:** Xung đột logic giữa ô Tìm kiếm và bộ lọc Thể loại, hệ thống bỏ qua điều kiện lọc danh mục khi người dùng nhập từ khóa (Xung đột Search & Filter)

**Môi trường:**

- Trình duyệt: Chrome Version 125.0.0
- Hệ điều hành: Windows / macOS
- Ứng dụng: Hệ thống Mượn sách thư viện (https://stqa.rbc.vn)

**Điều kiện tiên quyết:**

- Người dùng đã đăng nhập thành công vào hệ thống.
- Đang ở giao diện trang chủ hiển thị danh sách sách và bộ lọc phân loại.

**Bước tái hiện:**

1. Tại thanh công cụ lọc danh mục, nhấp chọn bộ lọc Thể loại là **"Kinh tế"**.
2. Tại ô tìm kiếm sách ngay phía trên, nhập vào từ khóa của một cuốn sách thuộc thể loại Công nghệ: `"Flutter"`.
3. Tiến hành thực thi tìm kiếm và quan sát danh sách kết quả hiển thị trên màn hình.

**Kết quả mong đợi:**
Hệ thống phải áp dụng kết hợp đồng thời cả hai điều kiện lọc theo logic toán tử `AND` (Thể loại = Kinh tế AND Từ khóa = Flutter). Do sách Flutter thuộc nhóm Công nghệ chứ không phải Kinh tế, hệ thống bắt buộc phải trả về màn hình trống và hiển thị thông báo "Không tìm thấy sách".

**Kết quả thực tế:**
Hệ thống bỏ qua hoàn toàn bộ lọc "Kinh tế" đang kích hoạt trước đó và ghi đè bằng kết quả của ô tìm kiếm, hiển thị cuốn sách "Lập trình Flutter cơ bản" (thuộc thể loại Công nghệ) lên màn hình kết quả.

**Tác động:**
Vi phạm nghiêm trọng logic nghiệp vụ kết hợp điều kiện lọc (Multi-criteria Filtering). Khiến tính năng phân loại theo danh mục bị vô hiệu hóa khi tìm kiếm, trả về kết quả sai lệch và gây nhiễu loạn thông tin đối với người dùng.

**Mức độ:**
**Cao (High)** — Lỗi logic nghiệp vụ (Business Logic Bug). Làm sai lệch hoàn toàn tính năng kết hợp điều kiện tìm kiếm nâng cao theo đặc tả hệ thống.

**Minh chứng:**

- Ảnh chụp màn hình đính kèm: `evidence/bug_12.png` _(Hiển thị thanh dropdown đang chọn "Kinh tế" nhưng kết quả bên dưới lại hiện sách "Công nghệ")_.

**Đề xuất xử lý:**
Cập nhật lại hàm xử lý truy vấn dữ liệu (Query Logic) ở Backend hoặc hàm Filter ở Frontend. Đảm bảo rằng cấu trúc điều kiện lấy dữ liệu phải truyền đồng thời cả 2 tham số: `where thể_loại = selected_category AND tên_sách LIKE %keyword%`, thay vì để hàm này ghi đè lên hàm kia.

---

## 5. BUG-REQ04-01: Thành viên có thể mượn sách vượt quá giới hạn cho phép (Tối đa 3 cuốn)

**Bug ID:** BUG-05 (Tham chiếu: TC-04-04)

**Tiêu đề:** Hệ thống không chặn giới hạn số lượng sách mượn tối đa của Thành viên, cho phép mượn đến cuốn thứ 4 và thứ 5 thành công mà không có thông báo lỗi

**Môi trường:**

- Trình duyệt: Chrome (Phiên bản mới nhất)
- Hệ điều hành: Windows 11
- Ứng dụng: Hệ thống Mượn sách thư viện (https://stqa.rbc.vn)

**Điều kiện tiên quyết:**

- Hệ thống đang ở trạng thái dữ liệu gốc.
- Tài khoản Thành viên đang ở trạng thái hoạt động bình thường (Active).

**Bước tái hiện:**

1. Truy cập hệ thống https://stqa.rbc.vn và tiến hành đăng nhập bằng tài khoản Thành viên: `dam.tran@email.com` / `password123`.
2. Tại màn hình danh sách sách, lần lượt nhấn nút "Mượn sách" (Borrow) cho 3 cuốn sách bất kỳ đang ở trạng thái "Sẵn sàng" (Ví dụ: `BOOK001`, `BOOK002`, `BOOK003`).
3. Tiếp tục tìm cuốn sách thứ 4 đang ở trạng thái "Sẵn sàng" (Ví dụ: `BOOK004`) và nhấn nút "Mượn sách".

**Kết quả mong đợi:**
Hệ thống phải kiểm tra số lượng sách đang mượn của tài khoản, chặn hành động mượn cuốn thứ 4 và hiển thị thông báo lỗi rõ ràng trên giao diện dạng Dialog/Toast theo đúng đặc tả SRS: "Đã đạt giới hạn mượn tối đa (3 cuốn)".

**Kết quả thực tế:**
Hệ thống không thực hiện kiểm tra giới hạn, vẫn cho phép tạo phiếu mượn thành công cho cuốn thứ 4 (và tiếp tục cho phép mượn thêm nhiều cuốn khác). Cuốn sách thứ 4 lập tức đổi nhãn trạng thái sang "Đang mượn" bình thường.

**Tác động:**
Vi phạm nghiêm trọng quy tắc nghiệp vụ (Business Rule) cốt lõi của thư viện được mô tả trong tài liệu đặc tả hệ thống SRS. Lỗi này dẫn đến nguy cơ thất thoát sách, mất kiểm soát tài nguyên và làm sai lệch nghiêm trọng số liệu vận hành.

**Mức độ:**
**Cao (High)** — Lỗi vi phạm nghiêm trọng logic nghiệp vụ hệ thống (Business Logic Bug). Làm hỏng cơ chế kiểm soát và ràng buộc dữ liệu quan trọng nhất của chức năng mượn sách.

**Minh chứng:**

- Ảnh chụp màn hình đính kèm: `evidence/bug_limit_maximum.png` _(Hiển thị danh sách phiếu mượn của tài khoản chứa từ 4 cuốn sách trở lên)_.

**Đề xuất xử lý:**
Bổ sung một hàm kiểm tra logic ràng buộc (Validation Check) trước khi phê duyệt tạo phiếu mượn mới: Thực hiện đếm tổng số phiếu mượn đang có trạng thái chưa trả của người dùng hiện tại (UserID), nếu kết quả lớn hơn hoặc bằng 3 thì lập tức chặn hành động và trả về mã lỗi thích hợp ở cả Frontend lẫn API Backend.

---

## 6. BUG-REQ05-01: Thiếu cơ chế xác nhận (Popup) và nút Hủy khi chọn Trả sách

**Bug ID:** BUG-06 (Tham chiếu: TC-05-05)

**Tiêu đề:** Hệ thống thực hiện hành động trả sách ngay lập tức khi click nút mà không hiển thị hộp thoại xác nhận (Popup/Modal Confirm) để người dùng kiểm tra lại

**Môi trường:**

- Trình duyệt: Chrome Version 125.0.0
- Hệ điều hành: Windows / macOS
- Ứng dụng: Hệ thống Mượn sách thư viện (https://stqa.rbc.vn)

**Điều kiện tiên quyết:**

- Người dùng đã đăng nhập thành công vào hệ thống bằng tài khoản Thành viên thông thường.
- Đang ở giao diện danh mục **"Phiếu mượn của tôi"** và tài khoản đang có phiếu mượn ở trạng thái "Đang mượn".

**Bước tái hiện:**

1. Di chuyển đến màn hình quản lý danh sách **"Phiếu mượn của tôi"**.
2. Tìm đến một bản ghi phiếu mượn bất kỳ đang ở trạng thái hiển thị là "Đang mượn".
3. Thực hiện nhấn chuột vào nút **"Trả sách"** và theo dõi phản hồi trực quan từ hệ thống.

**Kết quả mong đợi:**
Hệ thống bắt buộc phải hiển thị một hộp thoại (Dialog/Modal) cảnh báo để xác nhận hành vi của người dùng với thông điệp rõ ràng: _"Bạn có chắc chắn muốn thực hiện hành động trả cuốn sách này?"_ kèm theo 2 lựa chọn: **"Xác nhận"** và **"Hủy"**. Nếu nhấp chọn **"Hủy"**, tiến trình phải bị ngắt hoàn toàn và giữ nguyên trạng thái phiếu.

**Kết quả thực tế:**
Hệ thống xử lý trả sách thành công ngay lập tức và gửi API lên máy chủ mà không qua bất kỳ bước xác nhận trung gian nào từ phía người dùng, tước đi quyền hủy bỏ thao tác nếu lỡ bấm nhầm.

**Tác động:**
Lỗi nghiêm trọng về mặt trải nghiệm người dùng (UX Issue). Việc thiếu cơ chế xác nhận đối với các hành động mang tính thay đổi trạng thái dữ liệu (Data-mutating actions) rất dễ dẫn đến việc người dùng thao tác sai do bấm nhầm, làm mất dấu luồng nghiệp vụ mượn sách đang diễn ra.

**Mức độ:**
**Trung bình (Medium)** — Lỗi thiết kế tương tác giao diện và trải nghiệm (UX/Interaction Issue). Tiến trình xử lý dữ liệu logic của hệ thống vẫn chạy đúng bản chất nhưng không đảm bảo an toàn thao tác cho người dùng.

**Minh chứng:**

- Ảnh chụp màn hình đính kèm: `images/TC-05-05.png` _(Hiển thị màn hình phiếu mượn bị đổi trạng thái ngay sau khi click mà không có Popup hỏi lại)_.

**Đề xuất xử lý:**
Bổ sung một component Modal/Dialog xác nhận (Confirm Dialog) ở tầng Frontend để chặn sự kiện click chuột. Chỉ khi người dùng nhấp chọn nút đồng ý (Confirm) trong hộp thoại thì mới tiến hành kích hoạt hàm gọi API gửi về Backend.

---

## 7. BUG-REQ06-01: Bộ lọc trạng thái "Quá hạn" hoạt động sai logic, hiển thị sai dữ liệu

**Bug ID:** BUG-REQ06-01 (Tham chiếu: TC-06-03)

**Tiêu đề:** Bộ lọc danh mục hoạt động sai thuật toán, hiển thị lẫn lộn cả các phiếu mượn ở trạng thái "Đã trả" khi người dùng chọn tiêu chí lọc là "Quá hạn"

**Môi trường:**

- Trình duyệt: Chrome Version 125.0.0
- Hệ điều hành: Windows / macOS
- Ứng dụng: Hệ thống Mượn sách thư viện (https://stqa.rbc.vn)

**Điều kiện tiên quyết:**

- Người dùng đã đăng nhập thành công bằng tài khoản quyền **Thủ thư** (`librarian@library.com`).
- Hệ thống đang có sẵn cơ sở dữ liệu bao gồm cả phiếu mượn "Quá hạn" và phiếu mượn đã hoàn thành nghĩa vụ ("Đã trả").

**Bước tái hiện:**

1. Điều hướng người dùng đến trang quản trị chức năng **Quản lý phiếu mượn**.
2. Tìm đến thanh công cụ lọc dữ liệu, tại bộ lọc trạng thái (Dropdown Filter), nhấp chọn duy nhất một tiêu chí giá trị là **"Quá hạn"**.
3. Tiến hành xem xét kỹ nhãn hiển thị trạng thái của từng hàng kết quả vừa được hệ thống xuất ra trên bảng dữ liệu màn hình.

**Kết quả mong đợi:**
Khi bộ lọc trạng thái "Quá hạn" được áp dụng, hệ thống chỉ được phép truy vấn và xuất ra các phiếu mượn có đúng trạng thái "Quá hạn". Toàn bộ các bản ghi thuộc nhóm trạng thái khác (Đang mượn, Đã trả) bắt buộc phải được lọc sạch hoàn toàn khỏi màn hình hiển thị.

**Kết quả thực tế:**
Hệ thống trả về danh sách kết quả bị nhiễu loạn dữ liệu, hiển thị đồng thời cả các bản ghi có nhãn "Quá hạn" xen lẫn rất nhiều các bản ghi đã hoàn thành nghĩa vụ mang nhãn màu xanh "Đã trả".

**Tác động:**
Lỗi nghiêm trọng làm sai lệch tính năng báo cáo dữ liệu. Khiến Thủ thư bị rối loạn thông tin, không thể thống kê chính xác số lượng thành viên thực tế đang vi phạm thời gian mượn sách để gửi cảnh báo, làm giảm hiệu suất quản lý thư viện.

**Mức độ:**
**Cao (High)** — Lỗi logic nghiệp vụ hiển thị dữ liệu (Business & Query Data Logic Bug). Tính năng phân loại dữ liệu đầu ra bị hỏng, trả về sai tập dữ liệu yêu cầu của người dùng.

**Minh chứng:**

- Ảnh chụp màn hình đính kèm: `images/TC-06-03.jpeg` _(Hiển thị ô dropdown đang lọc chữ "Quá hạn" nhưng danh sách bên dưới vẫn hiện hàng loạt phiếu "Đã trả")_.

**Đề xuất xử lý:**
Kiểm tra lại câu lệnh truy vấn dữ liệu SQL (hoặc logic câu lệnh điều kiện Filter ở Backend). Chỉnh sửa điều kiện mệnh đề `WHERE` để đảm bảo hệ thống bóc tách chính xác trạng thái dựa trên mã định danh cụ thể (Ví dụ: `where status = 'OVERDUE'`), tránh việc viết sai điều kiện logic `OR` hoặc gộp nhầm nhóm dữ liệu cũ đã cập nhật.

---

## 8. BUG-REQ07-01: Bỏ lọt email sai định dạng

**Bug ID:** BUG-08 (Tham chiếu: TC-REQ07-02)

**Tiêu đề:** Hệ thống cho phép thêm thành viên thành công khi nhập email sai định dạng (thiếu dấu chấm trong phần domain)

**Môi trường:**

- Trình duyệt: Chrome Version 125.0.0
- Hệ điều hành: Windows / macOS
- Ứng dụng: Hệ thống Mượn sách thư viện (https://stqa.rbc.vn)

**Điều kiện tiên quyết:**

- Người dùng đã đăng nhập thành công bằng tài khoản **Thủ thư** (`librarian@library.com`).
- Đang truy cập ở màn hình **Thêm thành viên mới**.

**Bước tái hiện:**

1. Tại ô **Họ và tên**, nhập: `Vũ Sai Lỗi`.
2. Tại ô **Email**, nhập email thiếu dấu chấm (`.`) sau ký tự `@`: `loi.vu@email`.
3. Tại ô **Số điện thoại**, nhập: `0977333444`.
4. Nhấn nút **Thêm thành viên**.

**Kết quả mong đợi:**
Hệ thống từ chối tạo mới dữ liệu, hiển thị thông báo lỗi yêu cầu kiểm tra lại định dạng email (Do SRS quy định rõ: _"Email phải có dấu . trong phần domain"_).

**Kết quả thực tế:**
Hệ thống không phát hiện ra lỗi, vẫn chấp nhận lưu dữ liệu và hiển thị thông báo thêm thành viên thành công.

**Tác động:**
Dữ liệu rác, sai định dạng được đưa vào hệ thống cơ sở dữ liệu. Vi phạm quy tắc ràng buộc dữ liệu cơ bản, có thể gây lỗi cho các hệ thống gửi email tự động sau này.

**Mức độ:**
**Cao (High)** — Lỗ hổng trong việc Validate dữ liệu đầu vào, ảnh hưởng trực tiếp đến tính toàn vẹn và chính xác của dữ liệu (Data Integrity).

**Minh chứng:**

- Ảnh chụp màn hình đính kèm: `docs/assets/bug02-chap-nhan-email-sai.png` _(Hiển thị thông báo thêm thành công với email sai)_.

**Đề xuất xử lý:**
Bổ sung hoặc cập nhật lại biểu thức chính quy (Regex Validation) kiểm tra email. Bắt buộc phải có điều kiện kiểm tra sự tồn tại của ít nhất một dấu chấm (`.`) nằm ở phía sau ký tự `@` (Ví dụ: `@domain.com`).
