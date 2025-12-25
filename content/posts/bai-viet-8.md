---
title: "Bài 8: Xử lý ngoại lệ (Exception) khi lập trình mạng"
date: 2025-12-22
weight: 8
draft: false
tags: ["Java", "Best Practice"]
summary: "Mạng rớt, Server sập... làm sao để chương trình không bị Crash?"
---

Lập trình mạng rất rủi ro (dây cáp lỏng, wifi yếu...). Nếu không bắt lỗi, chương trình sẽ tắt cái rụp ngay lập tức.

Luôn luôn dùng khối `try-catch-finally` khi đụng tới Socket:

```java
Socket socket = null;
try {
    // Cố gắng kết nối
    socket = new Socket("localhost", 8080);
    System.out.println("Kết nối thành công!");
    
} catch (IOException e) {
    // Nếu lỗi thì chạy vào đây
    System.out.println("Lỗi kết nối: " + e.getMessage());
    
} finally {
    // Luôn luôn chạy vào đây để dọn dẹp
    try {
        if (socket != null) socket.close();
    } catch (Exception ex) {}
}