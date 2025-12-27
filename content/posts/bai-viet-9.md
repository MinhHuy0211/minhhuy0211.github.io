---
title: "Bài 9: Đa luồng (Multithreading) - Cách để Server tiếp 100 khách cùng lúc"
date: 2025-12-23
weight: 9
draft: false
tags: ["Java", "Multithreading", "Thread", "Server", "Concurrency"]
summary: "Giải thích tại sao server đơn luồng chỉ phục vụ được một client, và cách dùng đa luồng (hoặc Thread Pool) để xử lý hàng trăm kết nối đồng thời một cách hiệu quả."
thumbnail: "/sachhutech.jpg" # Thêm ảnh minh họa nếu có
---

Trong các bài trước, chúng ta đã viết server socket cơ bản. Nhưng nếu chạy thử với nhiều client, bạn sẽ thấy vấn đề lớn:  
**Khi một client đang kết nối và trao đổi dữ liệu, các client khác phải chờ đến lượt – thậm chí bị treo hoàn toàn!**

Đây chính là hạn chế của **server đơn luồng (single-threaded)**. Bài hôm nay sẽ giúp bạn biến server thành **đa luồng**, phục vụ hàng trăm client cùng lúc một cách mượt mà.

### 1. Tại sao server đơn luồng lại "chỉ tiếp được 1 khách"?
Hãy xem lại code server cơ bản:

```java
while (true) {
    Socket client = serverSocket.accept();  // Main thread BLOCK ở đây chờ client
    // Xử lý toàn bộ giao tiếp với client này (đọc + ghi + logic)
    handleClient(client);  // Trong lúc này, không client nào khác kết nối được!
    client.close();
}