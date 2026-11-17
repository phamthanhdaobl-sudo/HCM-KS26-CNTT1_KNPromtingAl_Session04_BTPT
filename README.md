# HCM-KS26-CNTT1_KNPromtingAl_Session04_BTPT
# BÁO CÁO: SO SÁNH TRADE-OFF CÁC GIẢI PHÁP RA LỆNH
## Kỹ thuật Prompting Nâng cao (Logic & Chuỗi)

**Họ và tên:** Phạm Thành Đạo  
**Lớp:** HCM-KS26-CNTT1

---

# I. GIỚI THIỆU BÀI TOÁN

## 1. Tên bài toán

So sánh hai phương án thiết kế Prompt cho AI Agent tự động xử lý đơn hàng trong cửa hàng thương mại điện tử.

## 2. Bối cảnh thực tế

Trong hoạt động kinh doanh trực tuyến, cửa hàng phải xử lý nhiều đơn hàng mỗi ngày. Thông tin đơn hàng có thể bị thiếu, sai định dạng hoặc không thống nhất, dẫn đến việc tính toán sai tổng tiền và phân loại sai trạng thái đơn hàng.

Để giải quyết vấn đề này, em đề xuất sử dụng AI Agent kết hợp các kỹ thuật Prompting nâng cao như Chain-of-Thought, Prompt Chaining và Context Anchoring.

Bài thực hành xây dựng hai phương án:

- **Giải pháp 1:** Prompt đơn giản, ngắn gọn, ít ràng buộc.
- **Giải pháp 2:** Prompt chi tiết, chia thành nhiều bước và có điều kiện xử lý lỗi.

## 3. Mục tiêu

- So sánh hiệu quả của hai cách thiết kế Prompt.
- Đánh giá khả năng xử lý dữ liệu thiếu và sai lệch.
- Xác định mức độ chính xác và tính ổn định của kết quả.
- Lựa chọn phương án phù hợp nhất với bài toán thực tế.

# II. BƯỚC 1: ĐỀ XUẤT HAI PROMPT MẪU

## 1. Giải pháp 1 – Prompt đơn giản

**Mục đích:** Sử dụng câu lệnh ngắn gọn để AI nhanh chóng tiếp nhận và xử lý đơn hàng.

**Prompt mẫu:**

```text
Bạn là trợ lý AI hỗ trợ xử lý đơn hàng cho cửa hàng
thương mại điện tử.

Hãy đọc thông tin đơn hàng khách hàng cung cấp,
kiểm tra các thông tin cơ bản, tính tổng tiền bằng
cách lấy số lượng nhân đơn giá cộng phí vận chuyển.

Sau đó, phân loại đơn hàng theo trạng thái thanh toán
và đưa ra đề xuất xử lý.

Nếu thiếu dữ liệu, hãy thông báo cho nhân viên.
Nếu dữ liệu không hợp lệ, hãy cảnh báo lỗi.

Trình bày kết quả ngắn gọn, dễ hiểu theo các mục:
- Mã đơn hàng.
- Khách hàng.
- Sản phẩm và số lượng.
- Tổng tiền.
- Trạng thái đơn hàng.
- Lỗi phát hiện.
- Đề xuất xử lý.
```

**Đặc điểm:**

- Câu lệnh ngắn, dễ viết và dễ sử dụng.
- Không yêu cầu AI thực hiện quá nhiều bước kiểm tra.
- Tiết kiệm token và thời gian xử lý.
- Có thể phù hợp với những đơn hàng đơn giản, ít rủi ro.

## 2. Giải pháp 2 – Prompt chi tiết, nhiều ràng buộc

**Mục đích:** Xây dựng quy trình xử lý có cấu trúc rõ ràng, kiểm tra dữ liệu theo từng bước và hạn chế lỗi phát sinh.

**Prompt mẫu:**

```text
VAI TRÒ:
Bạn là AI Agent chuyên xử lý đơn hàng cho cửa hàng
thương mại điện tử.

MỤC TIÊU:
Tiếp nhận, kiểm tra, tính toán và phân loại đơn hàng
với độ chính xác cao.

QUY TRÌNH XỬ LÝ:

BƯỚC 1: TRÍCH XUẤT
Đọc dữ liệu và xác định:
- Mã đơn hàng.
- Tên khách hàng.
- Số điện thoại.
- Tên sản phẩm.
- Số lượng.
- Đơn giá.
- Phí vận chuyển.
- Trạng thái thanh toán.
- Địa chỉ giao hàng.

BƯỚC 2: KIỂM TRA DỮ LIỆU
- Không được bỏ qua trường dữ liệu bị trống.
- Số lượng phải là số nguyên dương.
- Đơn giá và phí vận chuyển không được âm.
- Số điện thoại phải đúng định dạng.
- Trạng thái thanh toán chỉ chấp nhận:
  Đã thanh toán hoặc Chưa thanh toán.
- Nếu dữ liệu mâu thuẫn, phải đánh dấu cần xác minh.

BƯỚC 3: XỬ LÝ ĐIỀU KIỆN
- Nếu thiếu dữ liệu quan trọng: CHỜ BỔ SUNG.
- Nếu dữ liệu sai hoặc mâu thuẫn: CẦN XÁC MINH.
- Nếu dữ liệu hợp lệ và chưa thanh toán:
  CHỜ THANH TOÁN.
- Nếu dữ liệu hợp lệ và đã thanh toán:
  CHỜ XỬ LÝ GIAO HÀNG.

Không tự suy đoán hoặc tạo thông tin thay thế.
Không xác nhận thanh toán nếu chưa có bằng chứng.

BƯỚC 4: TÍNH TOÁN
Chỉ tính toán khi số lượng, đơn giá và phí vận chuyển
đã hợp lệ.

Thành tiền = Số lượng × Đơn giá.
Tổng thanh toán = Thành tiền + Phí vận chuyển.

Kiểm tra lại kết quả trước khi xuất báo cáo.

BƯỚC 5: XUẤT KẾT QUẢ
Trình bày theo cấu trúc:
1. Mã đơn hàng.
2. Thông tin khách hàng.
3. Thông tin sản phẩm.
4. Thành tiền.
5. Tổng thanh toán.
6. Trạng thái kiểm tra.
7. Phân loại đơn hàng.
8. Lỗi phát hiện.
9. Đề xuất xử lý.

BƯỚC 6: DUY TRÌ NGỮ CẢNH
Nếu hội thoại bị gián đoạn:
- Tóm tắt dữ liệu đã tiếp nhận.
- Lưu trạng thái xử lý hiện tại.
- Liệt kê các lỗi chưa giải quyết.
- Xác định bước tiếp theo cần thực hiện.

Khi tiếp tục hội thoại, phải sử dụng dữ liệu
đã được cung cấp trước đó.
Không tự tạo dữ liệu còn thiếu.

RÀNG BUỘC:
- Không bỏ qua bất kỳ lỗi dữ liệu nào.
- Không tự ý thay đổi thông tin khách hàng.
- Không tính toán từ dữ liệu không hợp lệ.
- Không thực hiện hành động thanh toán hoặc giao hàng.
- Nếu không đủ căn cứ, ghi rõ CẦN NHÂN VIÊN XÁC MINH.
- Chỉ đưa ra kết luận dựa trên dữ liệu đầu vào.
- Cung cấp tóm tắt căn cứ cho kết luận thay vì trình bày
  toàn bộ suy nghĩ nội bộ.
```

**Đặc điểm:**

- Chia nhiệm vụ thành nhiều bước cụ thể.
- Có quy tắc kiểm tra và xử lý lỗi.
- Có khả năng duy trì ngữ cảnh khi hội thoại bị gián đoạn.
- Hạn chế AI tự suy đoán thông tin.
- Phù hợp với quy trình xử lý đơn hàng có nhiều tình huống phát sinh.

# III. BƯỚC 2: LẬP BẢNG SO SÁNH TRADE-OFF

## 1. Bảng so sánh tổng quan

| Tiêu chí | Giải pháp 1 (Đơn giản) | Giải pháp 2 (Chi tiết) |
|---|---|---|
| Độ dễ hiểu | Cao | Trung bình |
| Độ dài Prompt | Ngắn | Dài |
| Tốn token | Ít | Nhiều hơn |
| Tốc độ xử lý | Nhanh | Có thể chậm hơn |
| Khả năng kiểm tra dữ liệu | Cơ bản | Chi tiết |
| Chặn lỗi biên | Trung bình | Tốt |
| Xử lý dữ liệu trống | Có cảnh báo nhưng ít quy tắc | Có điều kiện cụ thể |
| Xử lý dữ liệu sai lệch | Chưa phân loại rõ | Phân loại rõ ràng |
| Duy trì ngữ cảnh | Hạn chế | Có cơ chế tóm tắt |
| Khả năng mở rộng | Trung bình | Cao |
| Độ ổn định | Phụ thuộc dữ liệu đầu vào | Có cấu trúc kiểm soát tốt hơn |

## 2. Phân tích ưu điểm và nhược điểm

### Giải pháp 1 – Đơn giản

**Ưu điểm:**
- Dễ xây dựng và triển khai.
- Ít tốn token.
- Tốc độ phản hồi nhanh.
- Dễ chỉnh sửa khi thay đổi yêu cầu.

**Nhược điểm:**
- Chưa quy định rõ từng trường hợp lỗi.
- Có thể bỏ sót dữ liệu bất thường.
- Chưa có quy trình khôi phục ngữ cảnh cụ thể.
- Kết quả có thể thiếu nhất quán khi gặp tình huống phức tạp.

### Giải pháp 2 – Chi tiết

**Ưu điểm:**
- Quy trình xử lý rõ ràng.
- Kiểm tra được nhiều trường hợp dữ liệu lỗi.
- Hạn chế việc AI tự suy đoán.
- Có khả năng tiếp tục công việc khi hội thoại bị gián đoạn.
- Dễ kiểm tra và đánh giá từng giai đoạn.

**Nhược điểm:**
- Prompt dài hơn và tốn nhiều token hơn.
- Thời gian xây dựng và bảo trì lâu hơn.
- Có thể gây quá tải chỉ dẫn nếu thiết kế quá phức tạp.
- Cần cập nhật khi nghiệp vụ cửa hàng thay đổi.

## 3. Phân tích Trade-off

Trade-off là sự đánh đổi giữa các yếu tố khi lựa chọn một giải pháp.

Trong bài toán này:

- Giải pháp 1 ưu tiên tốc độ, sự đơn giản và tiết kiệm tài nguyên nhưng phải chấp nhận khả năng kiểm soát lỗi còn hạn chế.
- Giải pháp 2 ưu tiên độ chính xác, khả năng kiểm soát và tính ổn định nhưng phải đánh đổi bằng độ dài Prompt và chi phí xử lý cao hơn.

Như vậy, không có một phương án tốt nhất trong mọi trường hợp. Việc lựa chọn phụ thuộc vào mức độ phức tạp và yêu cầu thực tế của công việc.

# IV. BƯỚC 3: LỰA CHỌN PHƯƠNG ÁN TỐI ƯU VÀ CHẠY THỬ

## 1. Phương án được lựa chọn

**Lựa chọn Giải pháp 2 – Prompt chi tiết, nhiều ràng buộc.**

Lý do lựa chọn:

- Cửa hàng thương mại điện tử có thể tiếp nhận nhiều đơn hàng với thông tin khác nhau.
- Một sai sót nhỏ về số lượng, đơn giá hoặc trạng thái thanh toán có thể ảnh hưởng đến kết quả xử lý.
- Giải pháp 2 có các điều kiện kiểm tra cụ thể và phân loại lỗi rõ ràng.
- Có cơ chế tóm tắt để duy trì công việc khi hội thoại bị gián đoạn.
- Mặc dù tốn nhiều token hơn nhưng đổi lại có khả năng kiểm soát quy trình tốt hơn.

Đối với bài toán có liên quan đến tiền bạc và thông tin giao hàng, em ưu tiên độ chính xác và khả năng phát hiện lỗi hơn tốc độ phản hồi.

## 2. Dữ liệu chạy thử

**Input:**

```text
Mã đơn hàng: DH005
Khách hàng: Nguyễn Văn D
Số điện thoại: 0912345678
Sản phẩm: Mít sấy
Số lượng: 4
Đơn giá: 50.000đ
Phí vận chuyển: 20.000đ
Thanh toán: Chưa thanh toán
Địa chỉ: TP.HCM
Ghi chú: Giao hàng trong giờ hành chính.
```

## 3. Kết quả AI phản hồi

```text
BÁO CÁO XỬ LÝ ĐƠN HÀNG

1. Mã đơn hàng: DH005

2. Khách hàng:
Nguyễn Văn D

3. Sản phẩm:
Mít sấy

4. Số lượng:
4 sản phẩm

5. Đơn giá:
50.000đ

6. Thành tiền:
4 × 50.000 = 200.000đ

7. Phí vận chuyển:
20.000đ

8. Tổng thanh toán:
200.000 + 20.000 = 220.000đ

9. Trạng thái kiểm tra:
HỢP LỆ

10. Phân loại đơn hàng:
CHỜ THANH TOÁN

11. Lỗi phát hiện:
Không phát hiện lỗi.
Các trường thông tin cần thiết đã được cung cấp.

12. Đề xuất xử lý:
Gửi thông báo xác nhận đơn hàng và hướng dẫn
khách hàng thực hiện thanh toán.

KẾT LUẬN:
Đơn hàng DH005 có thông tin hợp lệ.
Tổng giá trị cần thanh toán là 220.000đ.
Đơn hàng đang chờ khách hàng thanh toán.
```

## 4. Đánh giá kết quả chạy thử

| Tiêu chí | Kết quả |
|---|---|
| Trích xuất dữ liệu | Đầy đủ |
| Kiểm tra thông tin | Hợp lệ |
| Tính toán | Chính xác |
| Phân loại đơn hàng | Đúng trạng thái |
| Phát hiện lỗi | Không có lỗi |
| Đề xuất xử lý | Phù hợp |

Kết quả cho thấy Giải pháp 2 có thể xử lý đơn hàng theo đúng trình tự đã thiết kế, từ tiếp nhận dữ liệu đến kiểm tra, tính toán và đưa ra đề xuất.

# V. KẾT LUẬN

Qua việc xây dựng và so sánh hai phương án Prompt, em nhận thấy mỗi giải pháp đều có những ưu điểm và hạn chế riêng.

Giải pháp 1 phù hợp với các công việc đơn giản, ít rủi ro và cần phản hồi nhanh. Trong khi đó, Giải pháp 2 phù hợp với những quy trình phức tạp, cần kiểm soát dữ liệu và hạn chế sai sót.

Em lựa chọn Giải pháp 2 vì bài toán xử lý đơn hàng liên quan trực tiếp đến thông tin khách hàng và giá trị thanh toán. Việc bổ sung các điều kiện kiểm tra, quy trình xử lý từng bước và cơ chế duy trì ngữ cảnh giúp giải pháp đáng tin cậy hơn.

Qua bài tập, em hiểu rằng thiết kế Prompt hiệu quả không phải là viết càng dài càng tốt, mà là lựa chọn mức độ chi tiết phù hợp với yêu cầu thực tế. Người thiết kế cần biết cân bằng giữa tốc độ, chi phí, độ chính xác và khả năng kiểm soát lỗi để đạt được hiệu quả tối ưu.

**Bài học rút ra:** Một Prompt tốt không chỉ giúp AI hiểu nhiệm vụ mà còn phải dự đoán được các tình huống bất thường và hướng dẫn AI xử lý chúng một cách có hệ thống.
