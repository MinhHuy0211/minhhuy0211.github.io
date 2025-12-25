---
title: "Bài 5: WebSocket - Công nghệ sau các ứng dụng Chat Realtime"
date: 2025-12-19
weight: 5
draft: false
tags: ["JavaScript", "Network"]
summary: "Tại sao Facebook, Zalo lại dùng WebSocket thay vì HTTP thông thường?"
---

### Vấn đề của HTTP
HTTP hoạt động kiểu "Hỏi - Đáp". Client hỏi thì Server mới trả lời. Nếu Client im lặng, Server cũng im. Điều này không làm Chat được vì tin nhắn phải đến ngay lập tức.

### Giải pháp: WebSocket
WebSocket tạo ra một "đường ống" kết nối liên tục 2 chiều.
* Server có tin nhắn mới -> Bắn ngay về Client.
* Client không cần hỏi (Request) liên tục.

Trong JS, khởi tạo rất dễ:
```javascript
// Kết nối đến Server
const socket = new WebSocket('ws://localhost:8080');

// Lắng nghe sự kiện khi có tin nhắn đến
socket.onmessage = function(event) {
    console.log("Có tin nhắn mới: " + event.data);
};

// Gửi tin nhắn đi
socket.onopen = function() {
    socket.send("Hello Server, I am Trọng!");
};