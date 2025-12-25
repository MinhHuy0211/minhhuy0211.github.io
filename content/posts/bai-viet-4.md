---
title: "Bài 4: Hướng dẫn gửi File ảnh qua Socket trong Java"
date: 2025-12-18
weight: 4
draft: false
tags: ["Java", "Socket", "File Transfer"]
summary: "Gửi text thì dễ, gửi file nhị phân (ảnh, nhạc) thì phải dùng FileInputStream."
---

Để gửi một file ảnh từ Client lên Server, chúng ta không dùng `BufferedReader` được (vì nó đọc text), mà phải dùng dòng byte.

### Code phía Client (Gửi)
```java
// Đọc file từ ổ cứng
FileInputStream fis = new FileInputStream("anh-meo.jpg");
// Lấy luồng gửi ra mạng
OutputStream os = socket.getOutputStream();

byte[] buffer = new byte[4096];
int bytesRead;

// Vừa đọc file vừa đẩy ra mạng
while ((bytesRead = fis.read(buffer)) != -1) {
    os.write(buffer, 0, bytesRead);
}