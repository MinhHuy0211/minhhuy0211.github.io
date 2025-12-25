---
title: "Bài 7: Xử lý dữ liệu JSON trong JavaScript"
date: 2025-12-21
weight: 7
draft: false
tags: ["JavaScript", "JSON"]
summary: "Hai hàm quan trọng nhất khi làm việc với API."
---

Khi nhận dữ liệu từ Java Server trả về (thường là dạng chuỗi String), JS cần biến nó thành Object để dùng.

### 1. JSON.parse()
Biến chuỗi thành Object.
```javascript
let dataString = '{"id": 1, "name": "Trọng"}';
let user = JSON.parse(dataString);
console.log(user.name); // Kết quả: Trọng