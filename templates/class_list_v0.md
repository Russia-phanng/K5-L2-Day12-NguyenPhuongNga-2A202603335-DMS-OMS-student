# Danh sách lớp v0 — Nguyễn Phương Nga · G07

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**
Xóa 2 dòng ví dụ trước khi nộp.

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person (driver) | seat=driver; seatbelt (worn_correct, worn_incorrect, not_worn, unknown) | Định vị người lái và kiểm tra tình trạng thắt dây an toàn | Có (hình dạng cơ thể; dây an toàn tùy độ sáng/độ che khuất) |
| 2 | face | box + eye_left, eye_right (open, closed, unknown) | Phát hiện trạng thái mở/nhắm mắt để đánh giá mất tập trung hoặc buồn ngủ | Có, trừ khi bị phản xạ, kính râm tối hoặc che khuất |
| 3 | glasses | none, clear, sun, unknown | Phân biệt trạng thái đeo kính để hiệu chỉnh kỳ vọng nhìn mắt/phản xạ | Một phần (kính râm trên NIR đôi khi trông gần như trong suốt) |
| 4 | gaze_zone | road, mirror_l, mirror_r, mirror_c, cluster, center, lap, other | Xác định vùng nhìn (đường, gương, đồng hồ, màn hình, đùi...) để phát hiện xao nhãng | Có theo tư thế đầu/hướng mắt và ánh sáng khung hình |
| 5 | phone | state (held, mounted, lap) | Phát hiện sử dụng hoặc đặt điện thoại để cảnh báo mất tập trung lái xe | Có nếu thấy rõ ít nhất một phần hình dạng máy/cạnh/màn hình |
| 6 | hand | whose (driver, passenger); side (left, right); on_wheel (yes, no, unknown) | Theo dõi vị trí tay và tương tác vô lăng/khoang lái để nhận diện hành vi lái | Có theo hình dạng tay và vị trí trong khung hình |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person (cabin) | seat (driver, front_passenger, rear_left, rear_middle, rear_right); seatbelt | Đếm số người và vị trí ngồi theo xe để phục vụ cảnh báo dây an toàn/cabin | Có theo hình dạng phần cơ thể nhìn thấy được |
| 2 | child_seat | seat; occupied (no, unknown) | Nhận diện ghế trẻ em và trạng thái ghế để hỗ trợ giám sát hàng ghế sau | Có theo hình dạng và ngữ cảnh (IR-sim chỉ mô phỏng kênh/đèn) |
| 3 | infant_seat | seat; facing (rear, front) | Nhận diện ghế em bé (nôi xách) và chiều quay để phục vụ cấu hình an toàn/nhắc nhở | Có theo hình dạng và ngữ cảnh vị trí ghế |
| 4 | object | seat; type (bag, box, cup, other) | Nhận diện đồ vật mang theo trên ghế/cabin để tránh nhầm với người hoặc phát hiện vật để quên | Có theo hình dạng/ngữ cảnh; IR-sim không có màu và kém chi tiết vật liệu |
| 5 | face (OMS) | box | Hỗ trợ xác nhận sự hiện diện/định hướng đầu của người ngồi trong cabin | Có khi khuôn mặt hiển thị rõ trong khung hình |
| 6 | frame_meta | modality (rgb, ir); light (day, night, unknown); camera_blocked (yes, no) | Chuẩn hóa ngữ cảnh nguồn ảnh, điều kiện ánh sáng và tình trạng che camera khi huấn luyện/kiểm thử | Có cho modality/camera_blocked; SVIRO dùng light=unknown |

## 2 câu hỏi leo thang

Câu hỏi bạn muốn hỏi người viết guideline (hoặc khách hàng) vì guideline v1.0 chưa trả lời. Mỗi câu kèm **tên khung** làm ví dụ.

1. Câu hỏi: Trên bộ SVIRO OMS, khi ghế phụ có búp bê hình trẻ em ngồi, guideline mục 4.1 ghi `child_seat` cho "Cả ghế trẻ em, ghế đang trống" nhưng mục 4.2 liệt kê "ghế trẻ em trống: child_seat" và mục 3 ghi bộ ảnh không có trẻ em ngồi — quy chuẩn thống nhất giữa `child_seat` và `object` cho búp bê/mô hình là gì để tránh lệch giữa các annotator?
Khung ví dụ: S01_rgb.png / S01_ir.png
Bạn tạm gán thế nào và vì sao: Sau khi đối chiếu với bạn review chéo và rà soát 15 dòng `diff`, mình tạm gán `child_seat` cho ghế trẻ em theo cách hiểu mở rộng ở mục 4.1 và cập nhật vào `export_final_v2.zip` để đồng bộ với peer, đồng thời đưa vào câu hỏi leo thang để chốt rõ văn bản ở bản guideline 1.x.
2. Câu hỏi: Trên ảnh NIR xoay ~90° của Drive&Act, khi `cabin_check` cảnh báo vị trí trái/phải mắt theo trục ngang (`x`) vốn dành cho mặt nhìn thẳng, quy ước kiểm tra tự động cho ảnh xoay dọc theo trục `y` sẽ chuẩn hóa thế nào để không gây nhầm lẫn với lỗi `lr_flip` thật?
Khung ví dụ: D01.png / D02.png
Bạn tạm gán thế nào và vì sao: Mình giữ đúng nhãn trái/phải theo người trong ảnh (mắt trái có tọa độ `y` lớn hơn mắt phải trên ảnh xoay ~90° theo mục 3 và 4.6) và ghi chú giải thích rõ khi kiểm tra, vì gán theo cơ thể người thật mới phản ánh đúng hướng nhìn của tài xế.
