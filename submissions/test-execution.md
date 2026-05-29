# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin         |                                    |
| ----------------- | ---------------------------------- |
| **Nhóm** | Nhóm STQA-03            |
| **Ngày thực thi** | 23/05/2026                         |
| **Trình duyệt** | Chrome Version 125.0.0             |
| **Hệ điều hành** | Windows / macOS                    |

---

## Kết quả chi tiết

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
| ----- | -------------- | -------------------------- | --------------- | -------- | ---------- | --- |
| **TC-01-01** | REQ-01: Đăng nhập | Đăng nhập thành công với email và mật khẩu hợp lệ, chuyển sang trang chủ. | Hệ thống đăng nhập thành công, chuyển sang trang chủ. AppBar hiển thị đúng tên và vai trò. | **Pass** | <img width="3806" height="1999" alt="image" src="https://github.com/user-attachments/assets/a4269639-d797-46d1-9c71-c7be024383e8" />| Không có |
| **TC-01-02** | REQ-01: Đăng nhập | Từ chối đăng nhập với mật khẩu sai, báo lỗi "Mật khẩu không đúng". | Hệ thống từ chối đăng nhập, hiển thị đúng thông báo lỗi mật khẩu. | **Pass** | <img width="3807" height="1986" alt="image" src="https://github.com/user-attachments/assets/9f19f539-5d65-4109-b149-e5008436d733" />| Không có |
| **TC-01-03** | REQ-01: Đăng nhập | Từ chối đăng nhập với email không tồn tại, báo lỗi "Không tìm thấy thành viên". | Hệ thống từ chối đăng nhập, hiển thị chính xác thông báo lỗi tài khoản không tồn tại. | **Pass** | <img width="3840" height="2256" alt="image" src="https://github.com/user-attachments/assets/9d9844d2-0b26-467d-a913-878c42d27e4e" />| Không có |
| **TC-01-04** | REQ-01: Đăng nhập | Báo lỗi "Vui lòng nhập email và mật khẩu" khi bỏ trống trường nhập liệu. | Hiển thị đúng thông báo yêu cầu nhập liệu, không gửi request lên máy chủ. | **Pass** | <img width="3840" height="2256" alt="image" src="https://github.com/user-attachments/assets/12316d9b-c372-4f52-9365-46818b36d5c5" />| Không có |
| **TC-01-05** | REQ-01: Đăng nhập | Từ chối xử lý khi email sai định dạng (thiếu @ hoặc dấu .). | Giao diện chặn đăng nhập, báo lỗi định dạng email không hợp lệ. | **Pass** | <img width="3840" height="2256" alt="image" src="https://github.com/user-attachments/assets/43dd8012-8272-4ece-8608-e766005f7f5e" />| Không có |
| **TC-02-01** | REQ-02: Xem danh sách sách | Thẻ sách hiển thị rõ ràng và đầy đủ 5 trường thông tin theo đúng đặc tả SRS. | Mỗi thẻ sách hiển thị rõ ràng và đầy đủ 5 trường thông tin bắt buộc: Tên sách, Tác giả, Thể loại, Năm xuất bản và Trạng thái. | **Pass** | `N/A` | Không có |
| **TC-02-02** | REQ-02: Xem danh sách sách | Tài khoản Thành viên xem được danh sách sách bình thường dưới giao diện thân thiện. | Danh sách sách hiển thị bình thường, giao diện sạch sẽ, thân thiện và tối ưu cho việc tìm kiếm, mượn sách của Thành viên. | **Pass** | `N/A` | Không có |
| **TC-02-03** | REQ-02: Xem danh sách sách | Tài khoản Thủ thư xem được danh sách sách đi kèm các nút tính năng quản trị. | Danh sách sách hiển thị đầy đủ, chi tiết và có đi kèm các nút tính năng/công cụ quản trị hệ thống dành riêng cho Thủ thư. | **Pass** | `N/A` | Không có |
| **TC-02-04** | REQ-02: Xem danh sách sách | Trạng thái sách tự động đồng bộ và cập nhật theo thời gian thực (Real-time). | Trạng thái cập nhật tức thì trên màn hình các phiên làm việc khác khi có biến động từ user khác mà không cần tải lại trang. | **Pass** | `N/A` | Không có |
| **TC-03-01** | REQ-03: Tìm kiếm & Lọc sách | Tìm kiếm từ khóa chữ thường `"flutter"` trả về chính xác cuốn sách liên quan. | Hệ thống lọc chính xác và hiển thị cuốn sách phù hợp là "Lập trình Flutter cơ bản" lên màn hình. | **Pass** | `N/A` | Không có |
| **TC-03-02** | REQ-03: Tìm kiếm & Lọc sách | Hệ thống xử lý không phân biệt hoa thường, tìm `"FLUTTER"` ra kết quả giống chữ thường. | Hệ thống không xử lý chuẩn hóa, báo trống `"Không tìm thấy sách"` (Bị lỗi phân biệt hoa/thường). | **Fail** | <img src="evidence/bug_c_01.png" width="150"> | BUG-10 |
| **TC-03-03** | REQ-03: Tìm kiếm & Lọc sách | Tìm kiếm theo tên tác giả hiển thị chính xác các cuốn sách của tác giả đó. | Hệ thống bóc tách dữ liệu và lọc ra đúng danh sách các cuốn sách thuộc về tác giả đã nhập. | **Pass** | `N/A` | Không có |
| **TC-03-04** | REQ-03: Tìm kiếm & Lọc sách | Tìm kiếm từ khóa không tồn tại hiển thị thông báo "Không tìm thấy sách". | Màn hình hiển thị chính xác thông báo lỗi trống dữ liệu theo đúng kịch bản thiết kế. | **Pass** | `N/A` | Không có |
| **TC-03-05** | REQ-03: Tìm kiếm & Lọc sách | Áp dụng bộ lọc Thể loại `"Công nghệ"` chỉ hiển thị các sách thuộc nhóm Công nghệ. | Bộ lọc hoạt động tốt, danh sách hiển thị thu hẹp chuẩn xác và không bị lọt các thể loại khác. | **Pass** | `N/A` | Không có |
| **TC-03-06** | REQ-03: Tìm kiếm & Lọc sách | Thực hiện xóa từ khóa hoặc hủy bộ lọc giúp khôi phục danh sách sách mặc định ban đầu. | Thanh tìm kiếm rỗng, các bộ lọc được bỏ chọn; hệ thống tự động tải lại toàn bộ danh sách sách mặc định đầy đủ. | **Pass** | `N/A` | Không có |
| **TC-04-01** | REQ-04: Mượn sách | Thành viên mượn sách thành công, sách đổi trạng thái sang "Borrowed" và hệ thống tự động tạo một phiếu mượn mới. | Đăng nhập mượn sách thành công. Hệ thống hiển thị Toast thông báo thành công, nhãn trạng thái sách chuyển sang màu cam "Đang mượn" và tạo bản ghi phiếu mới. | **Pass** | `N/A` | Không có |
| **TC-04-02** | REQ-04: Mượn sách | Hệ thống thực hiện chặn hành động mượn sách đối với tài khoản đang ở trạng thái bị Tạm ngưng (Blocked). | Hệ thống nhận diện trạng thái tài khoản, chặn không cho mượn và hiển thị Dialog báo lỗi tài khoản bị tạm ngưng theo đúng kịch bản. | **Pass** | `N/A` | Không có |
| **TC-04-03** | REQ-04: Mượn sách | Hệ thống thực hiện chặn hành động mượn sách đối với tài khoản đang ở trạng thái đã Hết hạn (Expired). | Hệ thống chặn thao tác mượn thành công, xuất hiện hộp thoại Dialog thông báo lỗi tài khoản đã hết hạn trên giao diện. | **Pass** | `N/A` | Không có |
| **TC-04-04** | REQ-04: Mượn sách | Hệ thống thực hiện chặn hành động mượn từ cuốn thứ 4 trở đi (Giới hạn số lượng mượn tối đa là 3 cuốn). | Hệ thống không kiểm tra giới hạn, vẫn cho phép tài khoản tạo phiếu mượn thành công cuốn thứ 4 và thứ 5 bình thường mà không có thông báo chặn lỗi. | **Fail** | <img src="evidence/bug_limit_maximum.png" width="150"> | BUG-REQ04-01 |
| **TC-04-05** | REQ-04: Mượn sách | Vô hiệu hóa nút mượn (Disabled) trên giao diện đối với các cuốn sách đang ở trạng thái đã bị mượn hoặc thất lạc. | Nút "Mượn sách" của các cuốn sách đã có người mượn tự động bị làm mờ xám (disabled) và chặn hoàn toàn tương tác bấm chuột từ user. | **Pass** | `N/A` | Không có |
| **TC-05-01** | REQ-05: Trả sách | Thành viên thực hiện trả sách đúng hạn thành công, sách đổi trạng thái thành "Có sẵn" và không xuất hiện cảnh báo vi phạm. | Trả sách thành công. Hệ thống hiển thị Toast thông báo, nhãn trạng thái sách lập tức chuyển sang màu xanh "Có sẵn", không có cảnh báo. | **Pass** | <img src="images/TC-05-01.png" width="150"> | Không có |
| **TC-05-02** | REQ-05: Trả sách | Thành viên trả sách quá hạn thành công, hệ thống ghi nhận và hiển thị cảnh báo phạt vi phạm thời gian mượn. | Không tồn tại dữ liệu phiếu mượn quá hạn trên môi trường kiểm thử để thực hiện kịch bản (Thiếu tài nguyên tạo Data). | **Blocked** | `N/A` | Không có |
| **TC-05-03** | REQ-05: Trả sách | Hệ thống tự động ẩn nút "Trả sách" đối với các phiếu mượn đã hoàn thành nghĩa vụ trả sách từ trước. | Giao diện ẩn hoàn toàn nút "Trả sách" trên các phiếu mượn đã trả, ngăn chặn thành công việc người dùng thao tác bấm lại. | **Pass** | <img src="images/TC-05-03.jpeg" width="150"> | Không có |
| **TC-05-04** | REQ-05: Trả sách | Hệ thống tự động đẩy người dùng quay về màn hình Đăng nhập khi phiên làm việc (Session) hết hạn. | Hệ thống kiểm tra Session, chuyển hướng thành công người dùng về trang Login khi cố thao tác trả sách lúc hết hạn. | **Pass** | <img src="images/TC-05-04.png" width="150"> | Không có |
| **TC-05-05** | REQ-05: Trả sách | Khi người dùng chọn hủy thao tác trong Popup xác nhận, tiến trình bị ngắt và trạng thái phiếu mượn được giữ nguyên. | Hệ thống lập tức kích hoạt API trả ngay khi bấm nút, hoàn toàn không hiển thị hộp thoại xác nhận (Popup/Modal) để người dùng chọn Hủy. | **Fail** | <img src="images/TC-05-05.png" width="150"> | BUG-REQ05-01 |
| **TC-06-01** | REQ-06: Xử lý quá hạn | Hệ thống tự động quét và cập nhật trạng thái các phiếu mượn trễ hạn (bao gồm phiếu `BR001`) thành "Quá hạn". | Tiến trình quét tự động (Cron job) hoạt động chính xác, cập nhật thành công nhãn trạng thái của các phiếu trễ hạn (bao gồm `BR001`). | **Pass** | <img src="images/tc-06-01.png" width="150"> | Không có |
| **TC-06-02** | REQ-06: Xử lý quá hạn | Hệ thống thông báo có "0 phiếu quá hạn" và giữ nguyên dữ liệu khi không có thành viên nào vi phạm thời gian mượn sách. | Cơ sở dữ liệu môi trường test luôn tồn tại sẵn phiếu quá hạn từ trước, không thể làm sạch hoàn toàn tập dữ liệu để chạy case này. | **Blocked** | `N/A` | Không có |
| **TC-06-03** | REQ-06: Xử lý quá hạn | Khi Thủ thư chọn bộ lọc "Quá hạn", danh sách hiển thị trên màn hình quản trị chỉ được xuất ra duy nhất các phiếu đang quá hạn. | Bộ lọc hoạt động sai thuật toán, danh sách kết quả hiển thị lẫn lộn cả các bản ghi "Quá hạn" và các bản ghi đã hoàn thành ("Đã trả"). | **Fail** | <img src="images/TC-06-03.jpeg" width="150"> | BUG-REQ06-01 |
| **TC-06-04** | REQ-06: Xử lý quá hạn | Tài khoản Thành viên nhìn thấy rõ ràng các phiếu mượn quá hạn cá nhân của mình (Định dạng nhãn màu đỏ hoặc chữ in đậm). | Phiếu trễ hạn hiển thị rất trực quan trạng thái "Quá hạn" với nhãn màu đỏ cảnh báo trên giao diện cá nhân của Thành viên. | **Pass** | <img src="images/TC-06-04.jpeg" width="150"> | Không có |
| **TC-06-05** | REQ-06: Xử lý quá hạn | Tài khoản Thành viên không có quyền thấy nút xử lý quá hạn, cố tình truy cập trực tiếp qua đường dẫn URL sẽ bị hệ thống chặn. | Nút chức năng bị ẩn hoàn toàn trên UI. Khi cố tình sao chép dán trực tiếp link URL quản trị, hệ thống tự động đẩy từ chối về trang Login. | **Pass** | <img src="images/TC-06-05.jpeg" width="150"> | Không có |
| **TC-07-01** | REQ-07: Quản lý thành viên | Thủ thư thêm thành viên mới thành công với email hợp lệ (binh.ly@email.com). | Hệ thống từ chối thêm mới và báo lỗi đỏ "Email không hợp lệ" dù email hoàn toàn đúng định dạng. | **Fail** | <img width="2880" height="1704" alt="image" src="https://github.com/user-attachments/assets/163cbe87-bf2c-4621-a9c1-3108c98a9bc9" />| BUG-01 |
| **TC-07-02** | REQ-07: Quản lý thành viên | Chặn thêm mới và báo lỗi khi nhập email sai định dạng (loi.vu@email). | Hệ thống không bắt lỗi định dạng, vẫn chấp nhận và thông báo thêm thành viên thành công. | **Fail** | <img src="image-7.png" width="150"> | BUG-02 |
| **TC-07-03** | REQ-07: Quản lý thành viên | Chặn thêm mới khi nhập email đã tồn tại (ba.nguyen@email.com). | Hệ thống từ chối tạo mới, hiển thị đúng thông báo "Email đã tồn tại". | **Pass** | <img src="image-8.png" width="150"> | Không có |
| **TC-07-04** | REQ-07: Quản lý thành viên | Tài khoản thường không có nút Thêm mới, cố tình truy cập URL sẽ bị chặn. | Nút Thêm mới bị ẩn. Khi cố tình dán URL để truy cập, hệ thống tự động đẩy về màn hình chính, không cho phép truy cập. | **Pass** | <img src="image-9.png" width="150"> | Không có |
| **TC-08-01** | REQ-08: Tra cứu phiếu mượn | Đăng nhập tài khoản Thành viên (`dam.tran@email.com`), hệ thống chỉ hiển thị đúng 2 phiếu mượn cá nhân (`BR002`, `BR005`). | Đăng nhập thành công tài khoản Thành viên. Giao diện hiển thị đúng cấu trúc và chỉ xuất hiện duy nhất 2 phiếu mượn cá nhân cá thể hóa là BR002 và BR005. | **Pass** | <img width="2554" height="1393" alt="image" src="https://github.com/user-attachments/assets/ead0d1dd-60f1-4b46-b9ca-c33ee3686fa6" />| Không có |
| **TC-08-02** | REQ-08: Tra cứu phiếu mượn | Đăng nhập tài khoản Thủ thư, hiển thị đủ 5 phiếu. Nhấn nút quét quá hạn, phiếu `BR001` và `BR003` đổi sang màu đỏ "Quá hạn", SnackBar hiện thông báo. | Hệ thống hiển thị đủ cả 5 phiếu mượn của mọi thành viên. Sau khi bấm nút, trạng thái BR001 và BR003 chuyển đỏ, SnackBar hiển thị: "Đã cập nhật: 2 phiếu mượn quá hạn." | **Pass** | <img src="docs/assets/evidence-tc-req08-02.png" width="150"> | Không có |
| **TC-08-03** | REQ-08: Tra cứu phiếu mượn | Khối thông tin của phiếu (ví dụ `BR003`) hiển thị đầy đủ 5 trường thông tin, phông chữ ngay ngắn không chồng chéo, nhãn trạng thái trực quan. | Khối thông tin hiển thị rõ ràng, không bị lỗi font hay đè chữ. Đầy đủ mã phiếu, tên sách, tên người mượn, cặp ngày và nhãn trạng thái trực quan. | **Pass** | <img src="docs/assets/evidence-tc-req08-03.png" width="150"> | Không có |
| **TC-08-04** | REQ-08: Tra cứu phiếu mượn | Đăng nhập sai thông tin, hệ thống từ chối truy cập và chặn hoàn toàn không cho tiếp cận phân hệ tra cứu phiếu mượn. | Hệ thống báo lỗi đăng nhập, giữ nguyên màn hình đăng nhập và bảo mật thông tin, không để lộ dữ liệu tra cứu phiếu mượn ra ngoài. | **Pass** | <img src="docs/assets/evidence-tc-req08-04.png" width="150"> | Không có |
| **TC-08-05** | REQ-08: Tra cứu phiếu mượn | Đăng nhập tài khoản có trạng thái Tạm ngưng/Hết hạn nhưng không có phiếu nào, màn hình hiển thị thông báo trống: "Chưa có phiếu mượn nào." | Giao diện không hiện phiếu của người khác, hệ thống xử lý phân quyền tốt và hiển thị màn hình trống kèm dòng chữ thông báo: "Chưa có phiếu mượn nào." | **Pass** | <img src="docs/assets/evidence-tc-req08-05.png" width="150"> | Không có |

## Tổng hợp kết quả

| Chỉ số | Giá trị |
| :--- | :--- |
| Tổng số test case | **39** |
| Pass | **31** |
| Fail | **6** |
| Blocked | **2** |
| Not Run | **0** |
| **Tỷ lệ Pass** | **79.49%** |

### Kết quả theo nhóm chức năng

| Nhóm | Tổng TC | Pass | Fail | Blocked | Tỷ lệ Pass |
| :--- | :---: | :---: | :---: | :---: | :---: |
| REQ-01: Đăng nhập | 5 | 5 | 0 | 0 | 100.00% |
| REQ-02: Xem danh sách sách | 4 | 4 | 0 | 0 | 100.00% |
| REQ-03: Tìm kiếm & Lọc sách | 6 | 5 | 1 | 0 | 83.33% |
| REQ-04: Mượn sách | 5 | 4 | 1 | 0 | 80.00% |
| REQ-05: Trả sách | 5 | 3 | 1 | 1 | 60.00% |
| REQ-06: Xử lý quá hạn | 5 | 3 | 1 | 1 | 60.00% |
| REQ-07: Quản lý thành viên | 4 | 2 | 2 | 0 | 50.00% |
| REQ-08: Tra cứu phiếu mượn | 5 | 5 | 0 | 0 | 100.00% |
| **Tổng cộng** | **39** | **31** | **6** | **2** | **79.49%** |
