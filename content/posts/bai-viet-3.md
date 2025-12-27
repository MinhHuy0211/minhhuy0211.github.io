---
title: "Bài 3: Callback Hell trong JavaScript và cách né tránh"
date: 2025-12-17
weight: 3
draft: false
tags: ["JavaScript", "Async", "Callback Hell", "Promise", "Async/Await"]
summary: "Hiểu rõ Callback Hell là gì, tại sao nó nguy hiểm và các cách hiện đại để viết code async sạch sẽ, dễ đọc, dễ bảo trì."
thumbnail: "/sachhutech.jpg" # Thêm ảnh minh họa nếu có
---

Trong JavaScript, hầu hết các thao tác bất đồng bộ (asynchronous) như gọi API, đọc file, setTimeout… đều sử dụng **callback** từ thời ES5 trở về trước. Khi các tác vụ phụ thuộc lẫn nhau, code dễ rơi vào tình trạng lồng ghép quá mức – được cộng đồng đặt tên hài hước nhưng rất chính xác: **Callback Hell** (Địa ngục callback).

### 1. Callback Hell trông như thế nào?
Hãy tưởng tượng bạn cần thực hiện tuần tự 4 bước gọi API, mỗi bước phụ thuộc kết quả bước trước:

```javascript
// Ví dụ kinh điển của Callback Hell
getUser(function(user) {
    getProfile(user.id, function(profile) {
        getPosts(profile.id, function(posts) {
            getComments(posts[0].id, function(comments) {
                getLikes(comments[0].id, function(likes) {
                    console.log("Cuối cùng cũng xong:", likes);
                });
            });
        });
    });
});