---
title: "Bài 8: Xử lý ngoại lệ (Exception) khi lập trình mạng trong Java"
date: 2025-12-22
weight: 8
draft: false
tags: ["Java", "Network", "Exception Handling", "Socket", "Best Practice"]
summary: "Hướng dẫn chi tiết cách xử lý ngoại lệ khi lập trình mạng để chương trình không crash khi gặp lỗi kết nối, đọc/ghi dữ liệu hay server sập."
thumbnail: "/sachhutech.jpg" # Thêm ảnh minh họa nếu có
---

Lập trình mạng là một trong những lĩnh vực **rủi ro nhất** trong Java. Lý do:
- Mạng có thể chập chờn (wifi yếu, dây lỏng).
- Server có thể tắt đột ngột.
- Client gửi dữ liệu sai định dạng.
- Firewall chặn port...

Nếu không xử lý ngoại lệ đúng cách, toàn bộ chương trình sẽ **crash ngay lập tức** với stack trace dài dằng dặc – trải nghiệm người dùng cực tệ.

Bài hôm nay sẽ giúp bạn biến chương trình mạng từ "dễ chết" thành **bền bỉ, chuyên nghiệp** bằng cách xử lý exception một cách thông minh.

### 1. Các ngoại lệ phổ biến khi lập trình mạng
| Ngoại lệ                     | Nguyên nhân thường gặp                              | Khi nào xảy ra?                          |
|------------------------------|-----------------------------------------------------|------------------------------------------|
| `UnknownHostException`       | Không tìm thấy hostname/IP                          | `InetAddress.getByName()`, kết nối sai IP |
| `ConnectException`           | Server từ chối kết nối (không có ai lắng nghe)      | `new Socket(...)` khi server chưa chạy   |
| `SocketTimeoutException`     | Timeout khi kết nối hoặc đọc dữ liệu                | `socket.setSoTimeout()`                  |
| `IOException`                | Lỗi chung I/O (mạng đứt, client đóng đột ngột...)   | Hầu hết các thao tác socket              |
| `SocketException`            | Socket bị đóng, reset bởi peer                      | Client/Server ngắt kết nối bất ngờ       |

### 2. Quy tắc vàng: Luôn dùng try-with-resources (Java 7+)
Đây là cách **tốt nhất và sạch nhất** để tự động đóng tài nguyên (socket, stream...) mà không cần viết `finally`.

```java
import java.net.*;
import java.io.*;

public class SafeClient {
    public static void main(String[] args) {
        String host = "localhost";
        int port = 8080;

        // Try-with-resources: tự động đóng socket và các stream
        try (Socket socket = new Socket(host, port);
             PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
             BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()))) {

            System.out.println("Kết nối thành công đến " + host + ":" + port);

            out.println("Hello Server từ Huy!");
            String response = in.readLine();
            System.out.println("Server trả lời: " + response);

        } catch (UnknownHostException e) {
            System.err.println("Không tìm thấy host: " + host);
        } catch (ConnectException e) {
            System.err.println("Không thể kết nối đến server. Server đang tắt hoặc port sai?");
        } catch (SocketTimeoutException e) {
            System.err.println("Timeout: Server không phản hồi kịp");
        } catch (IOException e) {
            System.err.println("Lỗi I/O: " + e.getMessage());
            // e.printStackTrace(); // Chỉ dùng khi debug
        }
    }
}