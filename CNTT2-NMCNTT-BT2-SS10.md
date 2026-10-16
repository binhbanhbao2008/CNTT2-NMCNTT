# **Báo cáo phân tích (I/O)**
- Input (đầu vào): Văn bản Markdown thô chứa nội dung hướng dẫn, câu lệnh Terminal, mã Python, bảng so sánh và danh sách kiểm tra thiết bị.
- Output (đầu ra): Tài liệu được render chuyên nghiệp, có tiêu đề rõ ràng, mã lệnh nổi bật, code Python có tô màu cú pháp, bảng so sánh và các ô checklist có thể đánh dấu.
- Mục đích: Giúp người đọc phân biệt nội dung giải thích với câu lệnh cần nhập và kiểm tra quá trình lắp đặt cảm biến độ ẩm.
```
sudo apt install -y git python3-pip
sudo pip3 install adafruit_DHT
```
```
sudo raspi-config      
# chọn: Interface Options >
# 1-wire > Enable
```
```
git clone https://github.com/adafruit/Adafruit_Python_DHT.git
cd Adafruit_Python_DHT/examples
```
```
python3 AdafruitDHT.py 22 4  
 # 22: DHT22, 4: GPIO pin
 # Nhận kết quả độ ẩm và nhiệt độ
```
```
crontab -e                   # Thêm dòng (ví dụ mỗi 5 phút):
                             # */5 * * * * python3 /home/pi/read_dht22.py
```

- 5 Kiểm tra kết quả    
```
Temp=28.4*   Humidity=67.1%
pi@farm:~$
```