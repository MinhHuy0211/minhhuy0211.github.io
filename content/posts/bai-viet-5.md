---
title: "Bài 5: WebSocket - Công nghệ sau các ứng dụng Chat Realtime"
date: 2025-12-19
weight: 5
draft: false
tags: ["JavaScript", "WebSocket", "Realtime", "Network"]
summary: "Tại sao các ứng dụng chat như Facebook, Zalo, Discord lại dùng WebSocket thay vì HTTP polling? Giải thích cơ chế hoạt động và cách dùng trong JavaScript."
thumbnail: "/sachhutech.jpg" # Thêm ảnh minh họa nếu có
---

Trong các ứng dụng chat thời gian thực (realtime chat), trò chơi online, thông báo đẩy, bảng điều khiển chứng khoán… người dùng cần nhận dữ liệu **ngay lập tức** khi có sự kiện xảy ra ở server mà không phải chờ đợi.

HTTP truyền thống không đáp ứng tốt yêu cầu này. WebSocket ra đời để giải quyết chính xác vấn đề đó.

### 1. Vấn đề của HTTP trong ứng dụng realtime
HTTP hoạt động theo mô hình **request-response** (hỏi - đáp):
- Client gửi request → Server trả response → kết nối đóng.
- Nếu muốn cập nhật dữ liệu mới, Client phải **hỏi lại** liên tục (gọi là Polling).

**Các cách "faking" realtime bằng HTTP:**
- **Short Polling**: Client hỏi server mỗi 1-2 giây ("Có tin nhắn mới không?").
- **Long Polling**: Client hỏi → Server giữ kết nối mở đến khi có dữ liệu mới → trả lời → Client hỏi lại ngay.

**Nhược điểm kinh khủng:**
- Tốn băng thông cực kỳ (hàng nghìn request vô ích).
- Độ trễ cao (phải chờ hết chu kỳ polling).
- Tải nặng server (hàng triệu kết nối long polling).
- Pin điện thoại mau hết, mạng chậm lag rõ rệt.

### 2. WebSocket – Giải pháp realtime thực thụ
WebSocket (định nghĩa trong RFC 6455) là giao thức cung cấp **kết nối full-duplex** (2 chiều) liên tục qua một kết nối TCP duy nhất.

**Nguyên lý hoạt động:**
1. Bắt đầu bằng một HTTP handshake (upgrade request).
2. Nếu server đồng ý → kết nối được "nâng cấp" thành WebSocket.
3. Từ đó trở đi, cả Client và Server có thể **gửi dữ liệu bất kỳ lúc nào** mà không cần request mới.
4. Kết nối giữ mở cho đến khi một bên đóng.

**Ưu điểm vượt trội:**
- Độ trễ cực thấp (tin nhắn đến gần như tức thì).
- Tiết kiệm tài nguyên (chỉ 1 kết nối thay vì hàng nghìn).
- Hỗ trợ truyền cả text và binary (gửi ảnh, file dễ dàng).
- Được hầu hết trình duyệt hiện đại hỗ trợ.

Các ông lớn dùng WebSocket: Facebook Messenger, Zalo, Discord, Slack, Trello, chứng khoán realtime, game online...

### 3. Sử dụng WebSocket trong JavaScript (Browser)
```javascript
// 1. Tạo kết nối WebSocket
const socket = new WebSocket('ws://localhost:8080');  // hoặc wss:// cho bảo mật

// 2. Sự kiện khi kết nối thành công
socket.onopen = function(event) {
    console.log("Kết nối WebSocket thành công!");
    socket.send("Hello Server! Tôi là Client đây!");
};

// 3. Nhận tin nhắn từ Server
socket.onmessage = function(event) {
    console.log("Tin nhắn từ Server:", event.data);
    
    // Nếu Server gửi binary (ví dụ ảnh)
    if (event.data instanceof Blob) {
        const url = URL.createObjectURL(event.data);
        document.body.innerHTML += `<img src="${url}" style="max-width:300px;">`;
    }
};

// 4. Xử lý lỗi
socket.onerror = function(error) {
    console.error("Lỗi WebSocket:", error);
};

// 5. Khi kết nối đóng
socket.onclose = function(event) {
    console.log("Kết nối đã đóng. Mã:", event.code, "Lý do:", event.reason);
};

// Gửi tin nhắn bất kỳ lúc nào
function sendMessage(msg) {
    if (socket.readyState === WebSocket.OPEN) {
        socket.send(msg);
    }
}