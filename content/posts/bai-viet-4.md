---
title: "Bài 4: Hướng dẫn gửi File ảnh qua Socket trong Java"
date: 2025-12-18
weight: 4
draft: false
tags: ["Java", "Socket", "File Transfer", "Network Programming"]
summary: "Hướng dẫn chi tiết cách truyền file nhị phân (ảnh, video, nhạc...) qua Socket bằng luồng byte, kèm code đầy đủ Client-Server và các lưu ý thực tế."
thumbnail: "/sachhutech.jpg" # Thêm ảnh minh họa nếu có
---

Trong các bài trước, chúng ta đã biết cách thiết lập kết nối Socket và gửi/nhận dữ liệu text đơn giản.  
Nhưng khi cần gửi **file nhị phân** như ảnh, video, nhạc, tài liệu PDF… thì không thể dùng `Reader/Writer` (dành cho text) nữa, vì chúng sẽ làm hỏng dữ liệu binary.

Thay vào đó, ta phải làm việc trực tiếp với **luồng byte** (`InputStream` / `OutputStream`).

Bài hôm nay sẽ xây dựng một ứng dụng **Client-Server hoàn chỉnh** để gửi một file ảnh từ Client lên Server và Server lưu lại.

### 1. Nguyên tắc truyền file qua Socket
- Client: Đọc file từ ổ cứng bằng `FileInputStream` → đẩy byte ra mạng qua `socket.getOutputStream()`.
- Server: Nhận byte từ mạng qua `socket.getInputStream()` → ghi vào file mới bằng `FileOutputStream`.
- Truyền theo **khối (chunk)** (thường 4KB - 64KB) để tránh tải toàn bộ file vào bộ nhớ.
- Nên gửi thêm **kích thước file** và **tên file** trước để Server biết cách lưu.

### 2. Code Server (Nhận file)
```java
import java.io.*;
import java.net.*;

public class FileServer {
    private static final int PORT = 8080;

    public static void main(String[] args) {
        try (ServerSocket serverSocket = new ServerSocket(PORT)) {
            System.out.println("Server đang chạy trên port " + PORT + "...");

            while (true) {
                Socket clientSocket = serverSocket.accept();
                System.out.println("Client kết nối: " + clientSocket.getInetAddress());

                new Thread(() -> handleClient(clientSocket)).start();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static void handleClient(Socket socket) {
        try (
            DataInputStream dis = new DataInputStream(socket.getInputStream());
            ) {
            // 1. Nhận tên file
            String fileName = dis.readUTF();
            // 2. Nhận kích thước file
            long fileSize = dis.readLong();

            // 3. Tạo file mới để lưu
            FileOutputStream fos = new FileOutputStream("received_" + fileName);
            BufferedOutputStream bos = new BufferedOutputStream(fos);

            byte[] buffer = new byte[8192];
            int bytesRead;
            long totalRead = 0;

            System.out.println("Đang nhận file: " + fileName + " (" + fileSize + " bytes)");

            // 4. Nhận và ghi dữ liệu
            while (totalRead < fileSize && (bytesRead = dis.read(buffer, 0, 
                (int) Math.min(buffer.length, fileSize - totalRead))) != -1) {
                bos.write(buffer, 0, bytesRead);
                totalRead += bytesRead;
            }

            bos.flush();
            System.out.println("Nhận file hoàn tất: " + fileName);

        } catch (IOException e) {
            System.err.println("Lỗi khi nhận file: " + e.getMessage());
        } finally {
            try { socket.close(); } catch (IOException e) {}
        }
    }
}