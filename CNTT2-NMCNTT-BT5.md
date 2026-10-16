# PHẦN 1: PHÂN TÍCH HỆ THỐNG TRANG TRẠI LAN

### 1. Xác định Input / Output của hệ thống
* **Input (Đầu vào):** 
  * Tín hiệu dữ liệu thô từ cảm biến nhiệt độ và độ ẩm không khí (DHT22), cảm biến độ ẩm đất.
  * Lệnh cấu hình ngưỡng tưới tự động hoặc lệnh thủ công từ người nông dân qua giao diện.
* **Output (Đầu ra):**
  * Tín hiệu điện đóng/mở van điện từ hoặc bật/tắt máy bơm nước.
  * Hiển thị thông số trực quan theo thời gian thực và cảnh báo trạng thái hệ thống.

### 2. Sơ đồ phối hợp phần cứng
```text
[ Cảm biến môi trường (DHT22) ] 
       │ (Dữ liệu thô)
       ▼
[ Vi điều khiển / SoC trung tâm (Raspberry Pi / ESP32) ] ◄──► [ Bộ nhớ RAM & Lưu trữ ]
       │ (Xử lý & Phát lệnh)
       ▼
[ Cơ cấu chấp hành (Máy bơm nước / Van điện từ) ]
```
# PHẦN 2: TRIỂN KHAI FILE README.md CHUẨN KỸ SƯ PHẦN MỀM
# 🚀 Smart-Farm IoT System

> *Hệ thống giám sát môi trường và tự động hóa tưới nước thông minh cho vườn lan của trang trại Lan, ứng dụng công nghệ IoT hiện đại.*

```

## 1. Hướng dẫn cài đặt (Installation)

Sử dụng các lệnh sau trong Terminal để thiết lập môi trường chạy chương trình đọc cảm biến:

```bash
# Tải mã nguồn từ kho lưu trữ GitHub
git clone https://github.com/adafruit/Adafruit_Python_DHT.git
cd Adafruit_Python_DHT/examples

# Chạy chương trình đọc cảm biến DHT22 tại chân GPIO số 4
python3 AdafruitDHT.py 22 4
2. Tính năng chính (Features)
[x] Giám sát nhiệt độ và độ ẩm không khí thời gian thực.

[x] Tự động hóa lịch trình tưới nước cho hoa lan dựa trên ngưỡng thiết lập.

[x] Ghi nhận nhật ký (Log) dữ liệu môi trường định kỳ vào hệ thống.

[ ] Tích hợp cảnh báo từ xa qua ứng dụng di động.

3. Bảng thông số kỹ thuật phần cứng (Specifications)
Tên thiết bị	Model / Linh kiện	Chức năng chính	Thông số hoạt động
Cảm biến	DHT22 (AM2302)	Đo nhiệt độ & độ ẩm không khí	Độ chính xác cao (±2% RH)
Bộ xử lý	Raspberry Pi 4	Điều phối và xử lý trung tâm	SoC Quad-core 1.5GHz
Cơ cấu chấp hành	Relay 5V & Van điện từ	Điều khiển hệ thống máy bơm nước	Điện áp 12VDC / 220VAC
4. Mô hình IPO & Chu kỳ xử lý lệnh tưới Lan
Chu kỳ Fetch – Decode – Execute (Tìm nạp – Giải mã – Thực thi) của CPU khi nhận lệnh tưới:

Fetch (Tìm nạp): CPU truy xuất lệnh điều khiển bật máy bơm từ bộ nhớ RAM vào thanh ghi lệnh.

Decode (Giải mã): Bộ giải mã xác định tín hiệu yêu cầu cấp nguồn cho chân GPIO điều khiển Relay.

Execute (Thực thi): Mạch điều khiển kích hoạt Relay đóng mạch, máy bơm nước chính thức hoạt động tưới cho vườn lan.

5. Quy trình chuyển hóa tri thức (Mô hình DIKW)
Quá trình hệ thống biến đổi dữ liệu thô thành hành động tưới nước thực tế:

Plaintext
       [ WISDOM (Sự khôn ngoan) ] ──► Tối ưu hóa mùa vụ, tiết kiệm nước tối đa cho trang trại
                 ▲
       [ KNOWLEDGE (Tri thức) ] ──► Quyết định: "Trời khô hạn, cần bật hệ thống tưới trong 10 phút"
                 ▲
     [ INFORMATION (Thông tin) ] ──► Xử lý: Nhiệt độ 32°C, độ ẩm không khí giảm còn 55%
                 ▲
        [ DATA (Dữ liệu thô) ] ──► Chỉ số thô từ cảm biến: 32, 55
6. Sơ đồ tổng quan hệ thống
7. Lưu ý vận hành an toàn
Xử lý khi RAM bị đầy dữ liệu nhật ký:
Khi bộ nhớ RAM hoặc phân vùng lưu trữ log ghi nhận tình trạng quá tải do lưu trữ quá nhiều dữ liệu cảm biến tạm thời, tuyệt đối không tắt nguồn đột ngột (Hard Reset) để tránh làm hỏng hệ thống file.

Cách xử lý an toàn: Tiến hành SSH vào thiết bị, kiểm tra các tiến trình ghi log đang chạy và thực hiện xóa bớt các file nhật ký cũ (/var/log/ hoặc bộ nhớ đệm tạm) bằng lệnh dọn dẹp hệ thống, hoặc khởi động lại dịch vụ (sudo systemctl restart smart-farm.service) sau khi đã sao lưu các dữ liệu quan trọng.
```

# PHẦN 3: KIỂM THỬ VÀ XỬ LÝ TÌNH HUỐNG (RAM ĐẦY)

Nội dung xử lý khi RAM đầy đã được tích hợp trực tiếp và hoàn thiện tại **Mục 7 (Lưu ý vận hành an toàn)** trong file README.md ở Phần 2. Giải pháp này giúp người quản lý tại trang trại Lan xử lý nhanh chóng tình trạng nghẽn bộ nhớ đệm mà không làm gián đoạn vận hành chung của hệ thống.