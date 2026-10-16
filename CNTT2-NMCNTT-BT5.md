# PHẦN 1: PHÂN TÍCH HỆ THỐNG TRANG TRẠI LAN

## 1. Xác định Input / Output của hệ thống
- **Input (Đầu vào - Dữ liệu thô từ cảm biến & người dùng):**
  - Tín hiệu độ ẩm đất, nhiệt độ và độ ẩm không khí từ các cảm biến DHT22 / Soil Moisture gắn tại các luống hoa lan.
  - Cài đặt ngưỡng tưới tự động hoặc lệnh thủ công từ người nông dân thông qua ứng dụng/giao diện điều khiển.
- **Output (Đầu ra - Hành động & Hiển thị):**
  - Tín hiệu điện đóng/mở van điện từ (Solenoid Valve) hoặc bật/tắt máy bơm nước.
  - Cảnh báo trực quan (đèn LED, còi hú) hoặc hiển thị thông số thời gian thực (Temp, Humidity) trên màn hình/giao diện Web.

## 2. Sơ đồ phối hợp phần cứng (Hardware Architecture)
```text
[ Cảm biến môi trường (DHT22) ] 
       │ (Dữ liệu thô: Nhiệt độ, Độ ẩm)
       ▼
[ Bộ xử lý trung tâm SoC (Raspberry Pi / ESP32) ] ◄──► [ Bộ nhớ RAM & Lưu trữ SSD ]
       │ (Ra quyết định & Gửi lệnh điều khiển)
       ▼
[ Thiết bị ngoại vi / Cơ cấu chấp hành (Máy bơm nước / Van điện từ) ]
PHẦN 2: TRIỂN KHAI FILE README.md CHUYÊN NGHIỆP(Đoạn mã dưới đây được tối ưu để render hoàn hảo trên StackEdit, sử dụng đầy đủ các thành phần Markdown theo yêu cầu).Markdown# 🚀 Smart-Farm IoT System

> Hệ thống giám sát môi trường và tự động hóa tưới nước thông minh cho vườn lan của trang trại Lan, ứng dụng công nghệ IoT và Điện toán biên hiện đại.

---

## 1. Hướng dẫn cài đặt (Installation)

Sử dụng các lệnh sau trong Terminal của Raspberry Pi để thiết lập môi trường chạy chương trình:

```bash
# Tải mã nguồn từ kho lưu trữ GitHub
git clone https://github.com/adafruit/Adafruit_Python_DHT.git
cd Adafruit_Python_DHT/examples

# Chạy chương trình đọc cảm biến DHT22 (Chân GPIO số 4)
python3 AdafruitDHT.py 22 4
2. Tính năng chính (Features)[x] Giám sát nhiệt độ và độ ẩm không khí thời gian thực.[x] Tự động hóa lịch trình tưới nước cho hoa lan dựa trên ngưỡng thiết lập.[x] Ghi nhận nhật ký (Log) dữ liệu môi trường định kỳ vào hệ thống.[ ] Tích hợp cảnh báo từ xa qua Telegram khi độ ẩm xuống thấp.3. Bảng thông số kỹ thuật phần cứng (Specifications)Tên thiết bịModel / Linh kiệnChức năng chínhThông số hoạt độngCảm biếnDHT22 (AM2302)Đo nhiệt độ & độ ẩm không khíĐộ chính xác cao ($\pm 2\%$ RH)Bộ xử lý trung tâmRaspberry Pi 4 Model BXử lý lệnh, điều phối ngoại viSoC Quad-core 1.5GHzCơ cấu chấp hànhRelay 5V & Van điện từĐiều khiển hệ thống máy bơm nướcĐiện áp 12VDC / 220VAC4. Mô hình IPO & Chu kỳ xử lý lệnh tưới LanChu kỳ Fetch – Decode – Execute (Tìm nạp – Giải mã – Thực thi) của CPU khi nhận lệnh tưới:Fetch (Tìm nạp): CPU truy xuất lệnh điều khiển bật máy bơm từ bộ nhớ RAM vào thanh ghi lệnh (Instruction Register).Decode (Giải mã): Bộ giải mã lệnh xác định đây là tín hiệu yêu cầu cấp nguồn cho chân GPIO điều khiển Relay máy bơm.Execute (Thực thi): ALU và mạch điều khiển phát dòng điện kích hoạt Relay đóng mạch, máy bơm nước chính thức hoạt động tưới cho vườn lan.5. Quy trình chuyển hóa tri thức (Mô hình DIKW)Quá trình hệ thống biến đổi dữ liệu thô thành hành động tưới nước thực tế:Plaintext       [ WISDOM (Sự khôn ngoan) ] ──► Tối ưu hóa mùa vụ, tiết kiệm nước tối đa cho trang trại
                 ▲
       [ KNOWLEDGE (Tri thức) ] ──► Quyết định: "Trời khô hạn, cần bật hệ thống tưới trong 10 phút"
                 ▲
     [ INFORMATION (Thông tin) ] ──► Xử lý: Nhiệt độ 32°C, độ ẩm không khí giảm còn 55%
                 ▲
        [ DATA (Dữ liệu thô) ] ──► Chỉ số thô từ cảm biến: 32, 55
6. Sơ đồ tổng quan hệ thống7. Lưu ý vận hành an toànXử lý khi RAM bị đầy dữ liệu nhật ký:Khi bộ nhớ RAM hoặc phân vùng lưu trữ log ghi nhận tình trạng quá tải (đầy bộ nhớ đệm do lưu quá nhiều dữ liệu cảm biến tạm thời), người vận hành tuyệt đối không tắt nguồn đột ngột (Hard Reset) để tránh làm hỏng hệ thống file.Cách xử lý an toàn: Tiến hành SSH vào thiết bị, kiểm tra các tiến trình ghi log đang chạy và thực hiện xóa bớt các file nhật ký cũ (/var/log/ hoặc bộ nhớ đệm tạm) bằng lệnh dọn dẹp hệ thống, hoặc khởi động lại tiến trình dịch vụ (sudo systemctl restart smart-farm.service) sau khi đã sao lưu các dữ liệu quan trọng lên bộ nhớ đám mây/SSD.
---

# PHẦN 2: KIỂM THỬ VÀ XỬ LÝ TÌNH HUỐNG (RAM ĐẦY)

Nội dung phần `Mục 7 (Lưu ý vận hành an toàn)` ở trên đã được bổ sung trực tiếp nhằm h