# Tự đánh giá — Nguyễn Phương Nga · G07

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_rgb.png | child_seat | missing | Ban đầu hiểu mục 4.2 theo hướng chỉ gán ghế trống nên không gán ghế có búp bê hình trẻ em | có |
| S01_rgb.png | child_seat | box | Có lệch/khác biệt bounding box (IoU=0.00 khi diff với peer) trên S01_rgb, đã rà soát và chốt lại trên export_final_v2.zip | có |
| S01_rgb.png | object | missing | Bổ sung các box object liên quan theo đối chiếu với peer và quy tắc 4.1 / 4.8 trên export_final_v2.zip | có |
| S01_ir.png | child_seat | missing | Thiếu box child_seat trên ảnh IR-sim ở bản đầu do cách hiểu mục 4.2, đã cập nhật vào export_final_v2.zip | có |
| S01_ir.png | object | missing | Thiếu box object trên ảnh IR-sim ở bản đầu, đã đối chiếu với S01_rgb và peer để cập nhật vào export_final_v2.zip | có |
| S03_rgb.png | infant_seat | missing | Ban đầu không gán ghế phụ có búp bê theo cách hiểu mục 4.2, sau đối chiếu peer đã cập nhật theo mục 4.1 / 4.8 | có |
| S03_rgb.png | object | missing | Bổ sung box object trên S03_rgb sau khi đối chiếu với peer và cập nhật export_final_v2.zip | có |
| S03_ir.png | infant_seat | missing | Bổ sung box infant_seat trên S03_ir theo đối chiếu với peer và cập nhật export_final_v2.zip | có |
| S03_ir.png | object | missing | Bổ sung box object trên S03_ir theo đối chiếu với peer và cập nhật export_final_v2.zip | có |
| S05_rgb.png | infant_seat | missing | Bổ sung box infant_seat trên S05_rgb theo đối chiếu với peer và cập nhật export_final_v2.zip | có |
| S05_rgb.png | object | missing | Bổ sung box object trên S05_rgb theo đối chiếu với peer và cập nhật export_final_v2.zip | có |
| S05_ir.png | infant_seat | missing | Bổ sung box infant_seat trên S05_ir theo đối chiếu với peer và cập nhật export_final_v2.zip | có |
| S05_ir.png | object | missing | Bổ sung box object trên S05_ir theo đối chiếu với peer và cập nhật export_final_v2.zip | có |
| S08_rgb.png | child_seat | missing | Bổ sung box child_seat trên S08_rgb theo đối chiếu với peer và cập nhật export_final_v2.zip | có |
| S08_rgb.png | object | missing | Bổ sung box object trên S08_rgb theo đối chiếu với peer và cập nhật export_final_v2.zip | có |
| S08_ir.png | child_seat | missing | Bổ sung box child_seat trên S08_ir theo đối chiếu với peer và cập nhật export_final_v2.zip | có |
| S08_ir.png | object | missing | Bổ sung box object trên S08_ir theo đối chiếu với peer và cập nhật export_final_v2.zip | có |
| D01.png | face / face13 / hand / person | ok | Đã kiểm tra đủ frame_meta, thuộc tính face, face13 và 4 box hand trên export_final_v2.zip (0 lỗi, 0 cảnh báo) | có |
| D02.png | face / face13 / hand / person | ok | Đã kiểm tra trên export_final_v2.zip (0 lỗi, 0 cảnh báo) | có |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Bỏ sót `child_seat`, `infant_seat` và `object` (`missing`) trên các cảnh OMS (`S01`, `S03`, `S05`, `S08`), kèm ca lệch `box` trên `S01_rgb.png`.

Vì sao mình mắc: Ban đầu bám cứng chữ "ghế trẻ em trống / ghế em bé trống" ở bảng 4.2 nên không đánh các ghế có búp bê hình trẻ em ngồi, dẫn tới thiếu box so với cách gán theo mục 4.1 và đối chiếu với các bạn.

Lần sau tránh bằng cách: Đối chiếu song song định nghĩa ở bảng 4.1 và quy tắc ở bảng 4.2 / mục 4.8, so sánh `diff` với bạn và chạy `cabin_check.py` kiểm tra lại trên bản export cuối (`export_final_v2.zip`).

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai. Mình học được gì từ dòng đó: Ở nhóm dòng `child_seat` / `infant_seat` / `object` trên các ảnh `S01`, `S03`, `S05`, `S08` (cả `_rgb` và `_ir`), khi đối chiếu với các bạn theo guideline, mình học được cách rà soát lại các vật thể/ghế xuất hiện ở bản của peer, phân biệt rõ ca đúng theo luật `4.8` với ca cần chỉnh sửa để chốt sang `export_final_v2.zip`.
