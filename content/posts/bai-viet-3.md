---
title: "Bài 3: Callback Hell trong JavaScript và cách né tránh"
date: 2025-12-17
weight: 3
draft: false
tags: ["JavaScript", "Async"]
summary: "Viết code JS lồng nhau quá nhiều sẽ tạo ra thảm họa."
---

Khi xử lý các tác vụ mạng (như gọi API), người mới học JS hay viết code lồng nhau kiểu này:

```javascript
// Cực hình Callback Hell
getData(function(a) {
    getMoreData(a, function(b) {
        getMoreData(b, function(c) {
            getMoreData(c, function(d) {
                console.log(d);
            });
        });
    });
});