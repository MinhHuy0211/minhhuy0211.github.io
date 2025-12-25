---
title: "Bài 9: Đa luồng (Multithreading) - Cách để Server tiếp 100 khách cùng lúc"
date: 2025-12-23
weight: 9
draft: false
tags: ["Java", "Thread", "Server"]
summary: "Nếu không có Đa luồng, Server của bạn chỉ phục vụ được đúng 1 người, người thứ 2 sẽ bị treo. Tại sao?"
---

Nếu bạn chạy code Server cơ bản, khi Client A kết nối, Server sẽ bận nói chuyện với A. Lúc này Client B kết nối tới sẽ bị "quay đều" (treo) cho đến khi A thoát ra.
=> Để khắc phục, ta phải dùng **Thread** (Luồng).

### Mô hình Server Đa luồng
Tưởng tượng Server là một ông chủ quán (Main Thread):
1.  Ông chủ đứng ở cửa (`socket.accept()`).
2.  Khách A tới => Ông chủ thuê nhân viên 1 ra tiếp A.
3.  Ông chủ quay lại cửa đứng chờ tiếp.
4.  Khách B tới => Ông chủ thuê nhân viên 2 ra tiếp B.

### Code minh họa (Java)

```java
while (true) {
    // 1. Chờ khách tới (Main Thread bị block ở đây)
    Socket clientSocket = serverSocket.accept();
    
    // 2. Có khách! Tạo một luồng riêng (Nhân viên) để xử lý
    Thread t = new Thread(new Runnable() {
        @Override
        public void run() {
            xuLyCongViec(clientSocket); // Nhân viên làm việc ở đây
        }
    });
    
    // 3. Đẩy nhân viên ra làm việc, ông chủ quay lại vòng lặp chờ khách mới
    t.start();
}