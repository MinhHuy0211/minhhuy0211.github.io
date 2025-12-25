---
title: "Bài 2: Port là gì? Tại sao Server hay dùng cổng 8080?"
date: 2025-12-16
weight: 2
draft: false
tags: ["Network", "Theory"]
summary: "Hiểu về khái niệm Port (Cổng) để tránh xung đột khi chạy phần mềm."
---

Nếu IP là địa chỉ nhà, thì **Port** chính là số phòng.
Một máy tính có thể chạy nhiều chương trình mạng (Web, Game, Chat...), mỗi chương trình phải có một Port riêng.

### Các loại Port phổ biến
* **Port 80:** Dành cho Web (HTTP).
* **Port 443:** Dành cho Web bảo mật (HTTPS).
* **Port 3306:** Dành cho MySQL Database.

### Lỗi thường gặp: "Address already in use"
Lỗi này xảy ra khi bạn cố mở Server ở một Port đang bị thằng khác chiếm dụng.
=> Cách sửa: Đổi sang số khác, ví dụ đổi từ 8080 sang 9999.