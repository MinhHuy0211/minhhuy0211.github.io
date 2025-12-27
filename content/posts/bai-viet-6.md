---
title: "Bài 6: Phân biệt Blocking IO và Non-Blocking IO"
date: 2025-12-20
weight: 6
draft: false
tags: ["Java", "Network", "IO", "Blocking", "Non-Blocking", "NIO", "Concurrency"]
summary: "Phân tích sâu sự khác biệt giữa Blocking IO và Non-Blocking IO, minh họa bằng code thực tế, so sánh hiệu suất và hướng dẫn khi nào nên dùng cái nào trong dự án Java."
thumbnail: "/sachhutech.jpg" # Thêm ảnh minh họa nếu có
---
Trong lập trình mạng Java, cách xử lý I/O (Input/Output) quyết định server của bạn có thể phục vụ **vài chục** hay **hàng chục nghìn** kết nối đồng thời. Hai mô hình chính là **Blocking IO** (truyền thống) và **Non-Blocking IO** (NIO – New IO).

Hiểu rõ sự khác biệt này là nền tảng để xây dựng các hệ thống hiệu năng cao như chat server, game online, API realtime hay microservices chịu tải lớn.

### 1. Blocking IO – Mô hình "chờ đợi" cổ điển
Đây là cách hoạt động mặc định của các class trong `java.io` và `java.net` (Socket, ServerSocket, InputStream, OutputStream...).

#### Đặc điểm chính
- Khi gọi các phương thức I/O như:
  - `serverSocket.accept()`
  - `inputStream.read()`
  - `outputStream.write()`
  
  → **Thread hiện tại bị block (dừng hoàn toàn)** cho đến khi thao tác hoàn tất hoặc có ngoại lệ.
- Thread không làm được việc gì khác trong lúc chờ.

#### Ví dụ Server Blocking đơn giản (chỉ xử lý 1 client tại 1 thời điểm)
```java
import java.net.*;
import java.io.*;

public class BlockingServer {
    public static void main(String[] args) throws IOException {
        ServerSocket serverSocket = new ServerSocket(8080);
        System.out.println("Server Blocking đang chạy...");

        while (true) {
            Socket client = serverSocket.accept();  // ← BLOCK: Đứng chờ client kết nối
            System.out.println("Client kết nối: " + client.getInetAddress());

            InputStream in = client.getInputStream();
            BufferedReader reader = new BufferedReader(new InputStreamReader(in));
            
            String line;
            while ((line = reader.readLine()) != null) {  // ← BLOCK: Chờ từng dòng từ client
                System.out.println("Nhận: " + line);
                if ("bye".equalsIgnoreCase(line)) break;
            }
            client.close();
        }
    }
}