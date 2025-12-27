---
title: "Bài 7: Xử lý dữ liệu JSON trong JavaScript – JSON.parse() và JSON.stringify()"
date: 2025-12-21
weight: 7
draft: false
tags: ["JavaScript", "JSON", "API", "parse", "stringify", "Frontend"]
summary: "Hướng dẫn chuyên sâu về hai hàm JSON.parse() và JSON.stringify() – công cụ không thể thiếu khi làm việc với API, fetch, localStorage và truyền dữ liệu Client-Server."
thumbnail: "/sachhutech.jpg" # Thêm ảnh minh họa nếu có
---

Trong phát triển web hiện đại, **JSON** (JavaScript Object Notation) là định dạng dữ liệu **chuẩn vàng** để trao đổi thông tin giữa Client (JavaScript) và Server (Java, Node.js, Python, PHP...).

Hầu hết mọi API RESTful đều trả về dữ liệu dạng JSON. Để JavaScript có thể đọc và thao tác dễ dàng, chúng ta cần chuyển đổi qua lại giữa **chuỗi JSON** và **object JavaScript**.

Hai "siêu anh hùng" thực hiện việc này chính là:
- `JSON.parse()` → **Chuỗi JSON → Object JS**
- `JSON.stringify()` → **Object JS → Chuỗi JSON**

Hiểu và dùng thành thạo hai hàm này sẽ giúp code của bạn sạch sẽ, chuyên nghiệp và tránh được rất nhiều lỗi ngớ ngẩn.

### 1. JSON.parse() – "Hồi sinh" dữ liệu từ chuỗi JSON
Khi gọi API bằng `fetch`, `axios` hay `XMLHttpRequest`, dữ liệu trả về thường là **chuỗi string** có định dạng JSON.

```javascript
// Dữ liệu giả lập nhận từ server
const jsonFromServer = `
{
  "id": 42,
  "name": "Huy",
  "age": 25,
  "isDeveloper": true,
  "skills": ["JavaScript", "Java", "React", "Node.js"],
  "address": {
    "city": "Hà Nội",
    "country": "Việt Nam"
  },
  "joinedDate": "2025-01-01"
}
`;

try {
    const user = JSON.parse(jsonFromServer);

    console.log("Object sau khi parse:", user);
    console.log("Tên:", user.name);                  // Huy
    console.log("Thành phố:", user.address.city);    // Hà Nội
    console.log("Kỹ năng đầu tiên:", user.skills[0]); // JavaScript
    console.log(typeof user);                        // object
} catch (error) {
    console.error("JSON không hợp lệ! Lỗi:", error.message);
}