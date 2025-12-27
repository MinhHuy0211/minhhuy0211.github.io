---
title: "Bài 2: Port là gì? Tại sao Server hay dùng cổng 8080?"
date: 2025-12-16
weight: 2
draft: false
tags: ["Java", "Network", "Port", "Socket"]
summary: "Giải thích rõ ràng khái niệm Port trong mạng máy tính, phân loại port, lý do dùng 8080 cho server dev và cách tránh xung đột port thực tế."
thumbnail: "/sachhutech.jpg"  # Thêm ảnh minh họa nếu có
---

Trong bài trước, chúng ta đã biết cách lấy IP của máy mình bằng `InetAddress`.  
Bây giờ, để hai chương trình có thể "nói chuyện" với nhau qua mạng, chỉ có IP là **chưa đủ**. Chúng ta cần thêm một thứ nữa: **Port** (cổng).

### Port là gì? Tại sao lại cần nó?
Hãy tưởng tượng IP là **địa chỉ nhà**, còn Port là **số phòng** trong ngôi nhà đó.

- Một máy tính (một IP) có thể chạy đồng thời rất nhiều dịch vụ mạng: trình duyệt web, game online, database, chat app, server phát triển…
- Mỗi dịch vụ sẽ **lắng nghe** trên một Port riêng biệt để nhận dữ liệu.
- Khi gửi dữ liệu, bạn phải chỉ rõ: "Gửi đến IP nào, Port nào" → hệ điều hành mới biết đưa gói tin cho đúng chương trình.

**Cấu trúc đầy đủ của một kết nối mạng**:  
`IP nguồn : Port nguồn  →  IP đích : Port đích`

Ví dụ: Khi bạn truy cập https://google.com  
- Máy bạn gửi yêu cầu từ IP của bạn + một Port ngẫu nhiên (ví dụ 54321)  
- Đến IP của Google + Port 443 (HTTPS)

### Phân loại Port (theo chuẩn IANA)
Port được chia thành 3 nhóm chính (tổng cộng 0 – 65535):

| Nhóm              | Dải Port       | Tên gọi              | Đặc điểm                                                                 |
|-------------------|----------------|----------------------|--------------------------------------------------------------------------|
| Well-known Ports  | 0 – 1023       | Port hệ thống        | Dành cho các dịch vụ chuẩn, cần quyền admin để bind (trên Linux/Windows) |
| Registered Ports  | 1024 – 49151   | Port đã đăng ký      | Các hãng phần mềm đăng ký dùng (MySQL: 3306, PostgreSQL: 5432...)       |
| Dynamic/Private   | 49152 – 65535  | Port động/tự do      | Dùng cho client kết nối tạm thời hoặc server dev tự do chọn             |

**Một số Port phổ biến cần nhớ:**
- 80 → HTTP (web không mã hóa)
- 443 → HTTPS (web có mã hóa)
- 21 → FTP
- 22 → SSH
- 25 → SMTP (gửi mail)
- 3306 → MySQL
- 5432 → PostgreSQL
- 27017 → MongoDB

### Tại sao developer hay dùng Port 8080 (hoặc 3000, 5000...)?
- Port dưới 1024 thường yêu cầu quyền **root/admin** → không tiện khi chạy thử nghiệm.
- Port 8080 là "người anh em" của Port 80 (HTTP), được IBM chọn làm port mặc định cho các proxy và server dev từ rất lâu → dần trở thành **thói quen toàn ngành**.
- Tương tự: Tomcat, Jetty, Spring Boot, GlassFish... đều mặc định 8080.
- Các port khác phổ biến trong dev:
  - 3000 → Node.js, React
  - 5000 → Python Flask
  - 8000 → Django
  - 9000 → PHP built-in server

### Lỗi kinh điển: "Address already in use" hoặc "Port already in use"
Khi bạn chạy server và thấy lỗi này, nghĩa là Port bạn chọn **đang bị chiếm** bởi một chương trình khác.

**Nguyên nhân thường gặp:**
1. Bạn đã chạy một instance server trước đó và chưa tắt.
2. Một phần mềm khác đang dùng port đó (ví dụ: Skype, Apache, Nginx... từng dùng 80/443).
3. Trên Mac/Windows: có dịch vụ hệ thống chiếm port.

**Cách khắc phục nhanh:**
- Đổi sang port khác: 8081, 9999, 3001...
- Tắt chương trình đang chiếm port.
- Trên Linux/Mac: Tìm và kill process
  ```bash
  lsof -i :8080          # Xem ai đang dùng port 8080
  kill -9 <PID>          # Kill process đó