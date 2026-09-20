# BÁO CÁO PHÂN TÍCH CƠ CHẾ PHÒNG NGỪA LỖI: THAO TÁC HỦY ĐƠN HÀNG

## Phần 1: Phân tích cơ chế phòng ngừa lỗi (Error Prevention)

Trong môi trường làm việc áp lực cao như xử lý hàng trăm đơn hàng mỗi ngày tại RikkeiShop Seller Center, nguyên tắc thiết kế **Error Prevention (Phòng ngừa lỗi)** và **User Control (Kiểm soát của người dùng)** là cực kỳ quan trọng để bảo vệ doanh thu của Nhà bán hàng. Dựa trên hiện trạng tại `image_f66a4d.png`
![alt text](image.png), chúng ta áp dụng 2 cơ chế chính để ngăn chặn bẫy bấm nhầm (Accidental Click):

**1. Phân cấp thị giác ở cấp độ danh sách (Visual Hierarchy):**
*   **Hiện trạng:** Nút "Xác nhận" và "Hủy" đang có cùng kích thước và độ đậm, khiến mắt người dùng không phân biệt được đâu là hành động chính (Happy Path), dẫn đến tỷ lệ click nhầm cao.
*   **Giải pháp:** Áp dụng sự tương phản. 
    *   Biến nút **"Xác nhận đơn"** thành **Primary Button** (Nút khối đặc, màu xanh dương) để thu hút sự chú ý, điều hướng Seller hoàn thành luồng công việc tích cực. 
    *   Hạ cấp nút **"Hủy đơn"** thành **Secondary Button** hoặc Text Button (Viền mỏng hoặc chỉ có chữ, màu trung tính như xám). Sự chênh lệch thị giác này giúp não bộ nhận diện luồng chính nhanh hơn và giảm thiểu thao tác lỗi.

**2. Tạo ma sát (Friction) có chủ đích bằng Modal Window:**
*   Hành động "Hủy đơn" là một thao tác nguy hiểm (Destructive Action). Nếu Seller vô tình bấm nhầm vào nút Hủy (đã được làm chìm), hệ thống vẫn không hủy ngay mà hiển thị **Modal Xác nhận**. Đây là lớp bảo vệ thứ hai.
*   **Cơ chế khóa an toàn (Forced Action):** Trong Modal này, nút xác nhận hủy cuối cùng bị vô hiệu hóa (Disabled) ở trạng thái mặc định. Người dùng **bắt buộc** phải thực hiện một thao tác có ý thức là mở Dropdown List và chọn "Lý do hủy đơn". Chỉ khi điều kiện này thỏa mãn, nút "Xác nhận hủy" (màu đỏ cảnh báo) mới được kích hoạt. Điều này loại bỏ hoàn toàn rủi ro người dùng bấm nhầm đúp 2 lần (double-click) gây hủy oan.

---

## Phần 2: Thiết kế Modal Window "Xác nhận hủy đơn" (Wireframe)

Dưới đây là cấu trúc phác thảo cho Modal Window, được thiết kế để đặt vào vùng trống trong wireframe `image_f66a4d.png`.
![alt text](image-1.png)

```text
+-------------------------------------------------------------------------+
|                                                                     [X] |
|                                                                         |
|                          XÁC NHẬN HỦY ĐƠN HÀNG                          |
|                                                                         |
|  Bạn đang thực hiện hủy đơn hàng RK20931 của khách hàng Nguyễn Văn A.   |
|  Lưu ý: Thao tác này không thể hoàn tác và có thể ảnh hưởng đến tỷ lệ   |
|  hoàn thành đơn của gian hàng.                                          |
|                                                                         |
|  Vui lòng chọn lý do hủy đơn (*):                                       |
|  +-------------------------------------------------------------------+  |
|  | Chọn lý do hủy...                                             [v] |  |
|  +-------------------------------------------------------------------+  |
|    (Dropdown options: Hết hàng, Sai giá, Người mua yêu cầu, v.v.)       |
|                                                                         |
|                                                                         |
|                                                                         |
|                +------------------+    +--------------------------+     |
|                |      Đóng        |    |      Xác nhận hủy        |     |
|                | (Nút viền xám)   |    | (Nút vô hiệu hóa/Xám) -> |     |
|                |                  |    | (Chuyển ĐỎ khi chọn lý do|     |
|                +------------------+    +--------------------------+     |
|                                                                         |
+-------------------------------------------------------------------------+
```

### Chi tiết ràng buộc UI trong thiết kế:
*   **Tiêu đề:** Rõ ràng, cho biết ngữ cảnh (Xác nhận hủy).
*   **Nội dung cảnh báo:** Nhắc lại mã đơn và tên khách hàng để Seller kiểm tra lại lần cuối xem có nhầm dòng không, kèm theo cảnh báo về hậu quả.
*   **Dropdown List:** Bắt buộc nhập (*).
*   **Nút "Đóng" (Cancel the action):** Cung cấp lối thoát an toàn (User Control) để Seller quay lại nếu nhận ra mình bấm nhầm.
*   **Nút "Xác nhận hủy" (Confirm Destructive Action):** Trạng thái ban đầu là Disabled. Sau khi Dropdown có giá trị, nút chuyển sang màu Đỏ (Màu tiêu chuẩn cho Destructive action) để cảnh báo thao tác nguy hiểm.

---

**Link Figma thiết kế Wireframe:** 
https://www.figma.com/design/mkT1v11WWZxuZi86p2itWF/Untitled?node-id=0-1&t=0ofovLEvne3ltaiB-1