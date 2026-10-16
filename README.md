# YOLOv8 Đếm Phương Tiện 🚗💨

> Đồ án sinh viên — Hệ thống đếm phương tiện giao thông trong video

Kho chứa này sử dụng YOLOv8 để phát hiện và đếm các phương tiện (ô tô, xe máy, xe tải, xe buýt) trong video. README này đã được viết bằng tiếng Việt và được tinh chỉnh theo cấu trúc hiện có của repo (`main.py`, `requirements.txt`, thư mục `assets`).

## Tổng quan

Luồng chính trong `main.py`:
- Tải mô hình YOLOv8 (mặc định: `yolov8m.pt`).
- Sử dụng DeepSORT (`deep-sort-realtime`) để theo dõi các đối tượng qua các khung hình.
- Đếm phương tiện khi tâm của bounding box đi qua một đường ngang cố định.
- Lưu video đầu ra `result.mp4` kèm chú thích và hiển thị thông tin đếm trên cửa sổ.

### Các lớp phương tiện (theo file `main.py`)
Trong mã nguồn, ánh xạ lớp được định nghĩa như sau (mã lớp COCO):
- 2 → Car (Ô tô)
- 3 → Motor (Xe máy)
- 5 → Bus (Xe buýt)
- 7 → Truck (Xe tải)

Nếu bạn dùng bộ class khác, hãy cập nhật từ điển `VEHICLES` trong `main.py`.

## Cấu trúc repository (hiện tại)

```
.
├── .gitignore
├── README.md        # (tệp này)
├── assets/          # chứa video mẫu (ví dụ: assets/video.mp4)
├── main.py          # script chính: chạy phát hiện, theo dõi, đếm
├── requirements.txt # phụ thuộc Python
```

## Yêu cầu

- Python 3.8+
- gói Python trong `requirements.txt` (đã bao gồm `ultralytics`, `opencv-python`, `deep-sort-realtime`, `numpy`, v.v.)
- GPU (tùy chọn, tăng tốc inference)

Cài đặt:

```bash
python -m venv venv
source venv/bin/activate      # macOS / Linux
# hoặc
venv\Scripts\activate        # Windows
pip install -r requirements.txt
```

Lưu ý: file `requirements.txt` đã liệt kê `ultralytics` và `deep-sort-realtime`.

## Chạy nhanh

Mặc định `main.py` đang đọc video từ `assets/video.mp4` và ghi kết quả ra `result.mp4`.

Chạy:

```bash
python main.py
```

Nếu muốn dùng video khác, chỉnh biến trong `main.py`:
- Dòng 16: thay `assets/video.mp4` bằng đường dẫn video của bạn.
- Dòng 6: nếu dùng trọng số khác, thay `yolov8m.pt` bằng `weights/best.pt` hoặc đường dẫn đến file .pt của bạn.
- Ngưỡng tin cậy: trong vòng lặp, mã bỏ qua detections có `conf < 0.5`. Có thể chỉnh giá trị này tùy ý.

## Tham số cấu hình quan trọng trong `main.py`
- LINE (dòng đếm): được tính từ chiều cao khung hình (mặc định là 60% chiều cao). Thay đổi tại dòng `LINE = int(original_h*0.6)`.
- OFFSET: vùng bù xung quanh đường đếm (mặc định 40 px). Điều chỉnh nếu camera có nhiều jitter.
- Ngưỡng confidence: hiện đang là `conf < 0.5` (bỏ detection có confidence thấp hơn 0.5).

## Đầu ra

- `result.mp4`: video được chú thích (bounding box, ID, class, tâm) và đường đếm.
- Trên cửa sổ hiển thị cũng sẽ in tổng số đối tượng đã được theo dõi (`Count`) và số lượng theo từng loại (Car, Motor, Bus, Truck).

Nếu bạn muốn xuất kết quả ra CSV (số lượng theo khung hoặc theo đoạn thời gian), tôi có thể bổ sung tính năng lưu file CSV.

## Gợi ý cải tiến

- Thêm tham số dòng lệnh (argparse) để dễ cấu hình (đường vào, đường ra, trọng số, ngưỡng confidence, v.v.).
- Lưu log/CSV cho phân tích sau này.
- Hỗ trợ nhiều lớp hơn hoặc ánh xạ tên lớp từ file cấu hình dataset.
- Thêm xử lý để reset bộ đếm cho video dài hoặc phân đoạn.

## Liên hệ

Tác giả: Bac Phan — email: phanvanbac15112005@gmail.com


---
