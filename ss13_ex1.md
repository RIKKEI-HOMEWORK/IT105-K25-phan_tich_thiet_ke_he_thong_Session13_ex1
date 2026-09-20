# BÁO CÁO PHÂN TÍCH TRADE-OFF VÀ ĐỀ XUẤT THIẾT KẾ BỘ LỌC RIKKEISHOP

## Phần 1: Đánh giá so sánh Trade-off

Với đặc thù của RikkeiShop là một sàn thương mại điện tử đa ngành hàng với hơn 50.000 sản phẩm và nhu cầu lọc kết hợp nhiều điều kiện sâu (Danh mục, Giá, Size, Màu sắc), dưới đây là bảng phân tích Trade-off giữa 2 giải pháp bố cục trên phiên bản Website Desktop:

|Tiêu chí đánh giá|(A) Cột bộ lọc bên trái (Sidebar Filter)|(B) Thanh bộ lọc ngang phía trên (Top Horizontal Bar)|
|-|-|-|
|**1. Không gian hiển thị (Display Space)**|**Nhược điểm:** Chiếm một phần diện tích chiều ngang cố định (thường từ 20-25% chiều rộng trang), làm giảm số lượng cột sản phẩm hiển thị trên một hàng (ví dụ: chỉ hiển thị được 3-4 sản phẩm/hàng thay vì 4-5).<br><br>**Ưu điểm:** Tối ưu không gian chiều dọc, không đẩy danh sách sản phẩm xuống quá sâu khỏi tầm mắt người dùng (above the fold).|**Ưu điểm:** Tối đa hóa không gian chiều ngang, cho phép lưới danh sách sản phẩm hiển thị rộng rãi hơn (4-5 sản phẩm/hàng).<br><br>**Nhược điểm:** Chiếm không gian chiều dọc. Nếu có nhiều bộ lọc, thanh này sẽ chiếm diện tích lớn ở phần đầu trang, đẩy các sản phẩm xuống dưới, buộc người dùng phải cuộn chuột nhiều hơn.|
|**2. Khả năng mở rộng (Scalability)**|**Ưu điểm vượt trội:** Khả năng mở rộng theo chiều dọc gần như vô hạn. Rất dễ dàng bổ sung thêm hàng chục nhóm tiêu chí lọc mới (như Thương hiệu, Chất liệu, Đánh giá sao, v.v.) dưới dạng Accordion (mở/thu gọn) mà không làm vỡ bố cục trang.<br><br>**Nhược điểm:** Nếu danh sách lọc quá dài, người dùng có thể phải cuộn chuột trong thanh sidebar để tìm tiêu chí mong muốn.|**Nhược điểm lớn:** Khả năng mở rộng rất kém. Khi số lượng tiêu chí tăng lên, thanh ngang sẽ bị quá tải, phải tràn xuống thành nhiều dòng (trông lộn xộn) hoặc phải ẩn vào nút "Thêm bộ lọc..." (làm tăng số lần click của người dùng). Các tiêu chí phức tạp như thanh trượt giá (Price Slider) hoặc bảng màu cũng khó hiển thị trực quan.|

### Đề xuất giải pháp tối ưu cho RikkeiShop:

**Lựa chọn: (A) Cột bộ lọc cố định bên trái (Sidebar Filter).**

*Lý do:* Theo bối cảnh bài toán, RikkeiShop có khối lượng sản phẩm khổng lồ và người dùng cần kết hợp rất nhiều tiêu chí cùng lúc ("Áo khoác nam, Màu đen, Size L, Giá từ 300.000 - 500.000 VNĐ"). Sidebar Filter cho phép hiển thị toàn bộ hoặc hầu hết các tùy chọn này để người dùng thao tác nhanh chóng, cung cấp trải nghiệm tốt nhất cho các truy vấn phức tạp. Ngoài ra, layout chia cột (bộ lọc bên trái, sản phẩm bên phải) là tiêu chuẩn quen thuộc của E-commerce, giúp người dùng dễ dàng làm quen.

\---

## Phần 2: Thiết kế khối Wireframe (Edge Case: Empty State)

Dựa trên yêu cầu, khi khách hàng áp dụng điều kiện lọc quá sâu dẫn đến kết quả trả về 0, hệ thống tuyệt đối không được để màn hình trắng. Thay vào đó, khu vực danh sách sản phẩm cần hiển thị một khối "Empty State".

### 2.1. Phác thảo cấu trúc UI (Wireframe Mockup)

Khối Empty State sẽ được căn giữa (center-aligned) bên trong khu vực danh sách sản phẩm:

```text
+-------------------------------------------------------------------------+
|                                                                         |
|                                                                         |
|                                \[ Icon ]                                 |
|                 (Hình kính lúp có dấu X hoặc hộp rỗng)                  |
|                                                                         |
|                    Không tìm thấy sản phẩm phù hợp                      |
|                                                                         |
|         Tiêu chí lọc của bạn đang quá hẹp. Vui lòng thử điều chỉnh      |
|             lại các tiêu chí hoặc xóa bộ lọc để xem thêm.               |
|                                                                         |
|                       +------------------------+                        |
|                       |   Xóa tất cả bộ lọc    |                        |
|                       +------------------------+                        |
|                                                                         |
|                                                                         |
+-------------------------------------------------------------------------+
```

### 2.2. Chi tiết các thành phần trong khối Empty State:

1. **Visual Graphic (Hình ảnh/Icon):** Một icon kích thước vừa phải, màu sắc trung tính (ví dụ: gray-400) để mô tả trạng thái trống (ví dụ: Kính lúp không tìm thấy đồ, hoặc hộp rỗng). Tránh dùng hình ảnh mang cảm xúc tiêu cực.
2. **Title (Tiêu đề):** Dòng chữ **"Không tìm thấy sản phẩm phù hợp"** — In đậm, kích thước lớn (Heading 3/4) để thông báo trực tiếp tình trạng cho người dùng.
3. **Subtitle (Mô tả phụ - Tùy chọn để tăng UX):** "Vui lòng thử điều chỉnh lại các tiêu chí hoặc xóa bộ lọc để xem thêm". Dòng này màu xám nhạt, giải thích lý do và hướng dẫn bước tiếp theo.
4. **Call-to-Action Button (Nút hành động chính):** Nút **"Xóa tất cả bộ lọc"** (Clear all filters). Nút này được thiết kế dạng Primary Button để thu hút sự chú ý. Khi click, hệ thống sẽ reset trạng thái của Sidebar bên trái và reload lại toàn bộ danh sách sản phẩm ban đầu.

\---

## Link thiết kế Figma:

https://www.figma.com/design/1jaMjyaK6tkhwcBfTYPvJH/Untitled?node-id=0-1\&t=jKMkMVL09fMBDUi6-1

