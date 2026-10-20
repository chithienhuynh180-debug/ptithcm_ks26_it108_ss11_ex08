# Bài: 5 quy tắc vàng database

## Phần 1: Phân tích lỗi

**1. các lỗi trong bảng**

| Vị trí | Lỗi | Quy tắc | Hậu quả với filter |
|--------|-----|---------|--------------------|
| hàng 1 | tiêu đề lớn bị merge, nằm trên hàng tên cột | 1 | filter không nhận đúng hàng tiêu đề |
| hàng trống sau dòng 2 và quanh dòng tổng | có hàng trống giữa dữ liệu | 4 | excel tưởng bảng hết ở đó nên chỉ lọc phần trên, ra 2 kết quả |
| dòng "TỔNG SỐ CNTT: 45" | dòng tổng nằm giữa dữ liệu | 5 | bị lẫn vào dữ liệu, chặn vùng lọc |
| ô "Trần Thị Bình  " | có dấu cách thừa ở cuối | 3 | filter coi là giá trị khác |

**2. lỗi khoảng trắng**

filter so sánh từng ký tự chính xác. dấu cách cũng là 1 ký tự nên "Trần Thị Bình  " khác "Trần Thị Bình". mắt nhìn thấy giống nhau nhưng filter coi là 2 giá trị riêng nên không khớp.

## Phần 2: Sửa lỗi

**3. cấu trúc bảng đúng**

| STT | Họ và Tên | Khoa / Viện | Điểm Xét Duyệt | Trạng Thái |
|-----|-----------|-------------|----------------|------------|
| 1 | Nguyễn Văn An | CNTT | 8.5 | Đã duyệt |
| 2 | Trần Thị Bình | CNTT | 7.9 | Chờ duyệt |
| 3 | Lê Minh Châu | Điện tử | 8.2 | Đã duyệt |

- tên cột nằm ở hàng 1, mỗi cột 1 ô riêng, không merge
- dữ liệu viết liền nhau từ hàng 2, xóa hết hàng trống
- tiêu đề lớn bỏ đi hoặc để ngoài bảng
- dòng tổng đặt ngoài bảng, ví dụ ô G1: `=COUNTIF(C2:C121,"CNTT")`
- ô nào thiếu dữ liệu thì ghi "chưa có" thay vì để trống

**4. trim và cách lọc**

- ô phụ F2 gõ `=TRIM(B2)` rồi kéo xuống hết cột
- copy cột F, paste values đè lên cột B rồi xóa cột F
- chọn cả bảng, bấm ctrl + shift + L
- cột Khoa Viện: bỏ chọn hết, chỉ tick CNTT
- cột Điểm Xét Duyệt: filter by condition, chọn "greater than or equal to", nhập 8.0
- kết quả là danh sách người vừa thuộc CNTT vừa có điểm từ 8.0 trở lên