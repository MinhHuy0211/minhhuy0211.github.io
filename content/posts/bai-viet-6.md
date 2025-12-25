---
title: "Bài 6: Phân biệt Blocking IO và Non-Blocking IO"
date: 2025-12-20
weight: 6
draft: false
tags: ["Java", "Theory"]
summary: "Khái niệm quan trọng để tối ưu hiệu năng Server."
---

### Blocking IO (Java IO cổ điển)
Khi chương trình chạy lệnh `socket.accept()` hoặc `in.read()`, nó sẽ **DỪNG LẠI** (Block) và chờ đợi.
* Nếu mạng lag hoặc Client chưa gửi gì, chương trình sẽ đứng hình ở đó luôn.
* **Hậu quả:** Server chỉ phục vụ được 1 người tại 1 thời điểm (nếu không dùng đa luồng).

### Non-Blocking IO (Java NIO)
Chương trình không bao giờ bị dừng. Nó sẽ kiểm tra liên tục:
* "Có dữ liệu không?"
* -> Nếu có: Xử lý ngay.
* -> Nếu không: Đi làm việc khác, lát quay lại kiểm tra tiếp.

**Kết luận:** Muốn Server chịu tải cao (hàng ngàn user) như Zalo/Facebook thì bắt buộc phải dùng Non-Blocking.