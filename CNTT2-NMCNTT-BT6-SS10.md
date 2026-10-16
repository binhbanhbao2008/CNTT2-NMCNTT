
# PHẦN 1: PHÂN TÍCH

### 1. Sai lầm trong tư duy của Nam khi dùng file Rich Text (.docx)
* **Sai lầm 1: Nhầm lẫn bản chất giữa Binary/XML Zip Archive và Plain Text.**
  * File `.docx` không phải là văn bản thô mà thực chất là một tập tin nén ZIP chứa nhiều file XML, hình ảnh và metadata định dạng bên trong. 
  * Khi lưu trữ mã nguồn hay tài liệu dự án trên hệ thống quản lý phiên bản như Git, Git xử lý `.docx` như một file nhị phân (Binary). Vì vậy, mỗi khi Nam chỉnh sửa dù chỉ một dấu phẩy, toàn bộ cấu trúc file nén bị thay đổi, khiến Git không thể theo dõi từng dòng lệnh/văn bản (line-by-line) mà báo xung đột (Conflict) toàn bộ file.

* **Sai lầm 2: Đánh đồng tính năng hiển thị của trình xử lý văn bản (Word) với môi trường xem trực tiếp (Web/Git).**
  * File Rich Text (.docx) phụ thuộc vào phần mềm chuyên dụng (như Microsoft Word) để giải nén và render giao diện. Do đó, trình duyệt hoặc GitHub không thể hiển thị trực tiếp nội dung file `.docx` nếu không có công cụ xem trước phức tạp.
  * Ngược lại, mã nguồn và tài liệu kỹ thuật ưu tiên khả năng đọc trực tiếp (Human-readable) mà không cần qua phần mềm đọc chuyên biệt.

---

### 2. Ưu thế của Markdown: An toàn, nhẹ hơn và chống hư hại file
* **Trọng lượng siêu nhẹ & Định dạng Plain Text:**
  * Markdown (`.md`) là văn bản thô (Plain Text) thuần túy, chỉ chứa các ký tự mã hóa chuẩn (ASCII/UTF-8) kết hợp với các ký hiệu định dạng đơn giản (`#`, `**`, `-`).
  * File Markdown không gánh các bộ định dạng nhị phân hay XML cồng kềnh, giúp dung lượng chỉ vài KB (nhẹ hơn hàng chục đến hàng trăm lần so với `.docx`).

* **Khả năng chống hư hại file (Đối chiếu bẫy dữ liệu):**
  * *Tệp Word (`.docx`):* Vì có cấu trúc nén chặt chẽ, nếu truyền qua mạng bị gián đoạn hay lỗi làm mất chỉ **1 byte** dữ liệu, toàn bộ cấu trúc nén ZIP/XML bị hỏng, dẫn đến lỗi "Corrupted File" và người dùng hoàn toàn không thể mở được file.
  * *Tệp Markdown (`.md`):* Do hoạt động theo cơ chế văn bản thô độc lập theo từng dòng/ký tự, nếu bị mất 1 byte dữ liệu trong quá trình tải, chỉ duy nhất ký tự đó bị lỗi hiển thị. Toàn bộ phần còn lại của văn bản vẫn hoàn toàn đọc được bình thường.

* **Tương thích tuyệt đối với Git Diff:**
  * So sánh văn bản theo từng dòng (Line-by-line diff), giúp các thành viên trong nhóm dễ dàng theo dõi chi tiết lịch sử thay đổi, nhận biết ai đã sửa câu/dòng nào và xử lý xung đột (Conflict) một cách chính xác, nhanh chóng.

---

# PHẦN 2: HOÀN THIỆN (FILE README.md CHUẨN STACKEDIT)

```markdown
# 🌿 Dự án GreenTech - Hệ Thống Nông Nghiệp Thông Minh

> **GreenTech** là giải pháp công nghệ tiên tiến ứng dụng IoT và Trí tuệ nhân tạo (AI) giúp tự động hóa quy trình chăm sóc cây trồng, tối ưu hóa lượng nước tưới và nâng cao năng suất trang trại.

---

## 📋 Mục tiêu dự án
* **Giám sát thời gian thực:** Đọc và phân tích các thông số nhiệt độ, độ ẩm không khí và độ ẩm đất.
* **Tự động hóa thông minh:** Tự động kích hoạt hệ thống tưới tiêu khi các chỉ số môi trường vượt ngưỡng cho phép.
* **Tối ưu tài nguyên:** Giảm thiểu chi phí nhân công và lượng nước tiêu thụ trong nông nghiệp.

```

## 🛠️ Cấu trúc phần cứng cốt lõi

| Thiết bị / Linh kiện | Loại / Model | Chức năng chính |
| :--- | :--- | :--- |
| **Bộ xử lý trung tâm** | Raspberry Pi 4 / ESP32 | Xử lý dữ liệu cảm biến và phát lệnh thực thi |
| **Cảm biến môi trường** | DHT22 / Soil Moisture Sensor | Thu thập nhiệt độ, độ ẩm không khí và độ ẩm đất |
| **Cơ cấu chấp hành** | Relay 5V & Van điện từ | Bật/Tắt hệ thống máy bơm tưới nước tự động |

```

## 🚀 Hướng dẫn khởi chạy nhanh

Để thiết lập môi trường và chạy dự án trên thiết bị, mở Terminal và thực hiện các lệnh sau:

```bash
# 1. Clone kho lưu trữ mã nguồn từ GitHub
git clone https://github.com/GreenTech-PTIT/GreenTech-System.git

# 2. Di chuyển vào thư mục dự án
cd GreenTech-System

# 3. Chạy chương trình giám sát chính
python3 main.py