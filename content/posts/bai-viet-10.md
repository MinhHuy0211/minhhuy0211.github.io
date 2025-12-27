---
title: "Bài 10: Tổng kết và Đánh giá kết quả Đồ án môn Lập trình mạng"
date: 2025-12-23
weight: 10
draft: false
summary: "Báo cáo tổng kết toàn bộ quá trình thực hiện đồ án xây dựng Blog cá nhân chuyên sâu về lập trình mạng, kết quả đạt được và những bài học quý giá."
thumbnail: "/sachhutech.jpg" # Thêm ảnh bìa đẹp nếu có
---

<style>
    /* 1. Căn chỉnh độ rộng khung nhìn (Vừa mắt, chuyên nghiệp) */
    .main, .post-single {
        max-width: 1100px !important;
        margin: 0 auto !important;
    }
    
    /* 2. Font chữ hiện đại, dễ đọc */
    body, .post-content {
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif !important;
        font-size: 18px !important;
        line-height: 1.85 !important;
        color: #222 !important;
    }
    
    .post-content {
        text-align: justify !important;
        text-justify: inter-word !important;
    }
    
    /* Tiêu đề lớn hơn, nổi bật */
    .post-title {
        text-align: center;
        font-size: 42px !important;
        font-weight: 900 !important;
        margin-bottom: 30px !important;
        letter-spacing: -1px;
    }
    
    h3 {
        margin-top: 50px !important;
        border-bottom: 2px solid #444 !important;
        padding-bottom: 12px !important;
        font-size: 26px !important;
    }
    
    /* Danh sách đẹp hơn */
    ul, ol {
        margin-left: 20px;
        padding-left: 20px;
    }
    
    li {
        margin-bottom: 12px;
    }
</style>

Đồ án môn **Lập trình mạng** là cơ hội tuyệt vời để em – **Huy** – vận dụng toàn bộ kiến thức lý thuyết vào thực tiễn, từ việc xây dựng một hệ thống website tĩnh chuyên nghiệp đến nghiên cứu sâu về các giao thức mạng, Socket, đa luồng và xử lý bất đồng bộ. Bài viết này tổng kết lại toàn bộ hành trình, kết quả đạt được và những bài học quý giá em đã rút ra.

### 1. Kết quả đạt được

Sau hơn 2 tháng nghiên cứu và thực hiện, đồ án đã hoàn thành xuất sắc các mục tiêu đề ra:

- **Xây dựng thành công Website cá nhân (Blog kỹ thuật):**  
  Sử dụng **Hugo** – Static Site Generator hiện đại, thiết kế giao diện tối giản, sang trọng, responsive hoàn hảo trên mọi thiết bị. Triển khai ổn định trên **GitHub Pages** với domain cá nhân.

- **Hoàn thành 09 bài viết chuyên sâu về môn học:**  
  Các bài viết đi sâu vào các chủ đề cốt lõi của Lập trình mạng:  
  - Socket cơ bản  
  - Gửi file nhị phân (ảnh) qua Socket  
  - WebSocket cho ứng dụng realtime  
  - Blocking vs Non-Blocking IO  
  - Multithreading trong server  
  - Xử lý ngoại lệ (Exception) khi lập trình mạng  
  - Xử lý JSON trong JavaScript  
  - Và nhiều kiến thức thực tiễn khác  

  Mỗi bài đều có **code minh họa đầy đủ**, giải thích chi tiết, kèm theo các best practice thực tế.

- **Áp dụng quy trình quản lý mã nguồn chuyên nghiệp:**  
  Sử dụng **Git Flow** (branch main, develop, feature) để quản lý phiên bản.  
  Commit rõ ràng, có mô tả chi tiết, dễ dàng rollback khi cần.

### 2. Kiến thức và kỹ năng tích lũy

Quá trình thực hiện đồ án không chỉ là viết code mà còn là hành trình học hỏi sâu sắc:

- **Hiểu rõ sự khác biệt giữa lý thuyết và thực tế:**  
  Trong sách vở, Socket đơn giản lắm. Nhưng khi triển khai thực tế, em gặp phải hàng loạt vấn đề: độ trễ mạng, ngắt kết nối đột ngột, quản lý tài nguyên, xử lý ngoại lệ… Những thứ này không có trong lý thuyết.

- **Nâng cao kỹ năng Debugging & Troubleshooting:**  
  Thành thạo đọc stack trace, sử dụng công cụ debug (IntelliJ, VS Code), phân tích log lỗi, tìm nguyên nhân từ `IOException`, `SocketTimeoutException`, `UnknownHostException`…

- **Viết code sạch, dễ bảo trì:**  
  Áp dụng Clean Code: đặt tên biến, hàm rõ ràng; sử dụng try-with-resources; tách logic xử lý client ra thread riêng; comment code chi tiết.

- **Kỹ năng làm việc với công cụ hiện đại:**  
  - Hugo + Markdown để viết blog  
  - GitHub Pages + GitHub Actions (tự động build & deploy)  
  - Tailwind CSS hoặc CSS thuần để thiết kế giao diện

- **Tư duy hệ thống:**  
  Hiểu rõ tại sao server đơn luồng không scale, tại sao Non-Blocking IO mạnh mẽ, tại sao Thread Pool quan trọng hơn tạo thread thủ công…

### 3. Đánh giá tự nhận

- **Đạt 100% mục tiêu đề ra** (xây dựng blog + 9 bài viết chuyên sâu).  
- **Chất lượng code cao**, có xử lý ngoại lệ, đa luồng, realtime… – vượt xa yêu cầu cơ bản của môn học.  
- **Trình bày rõ ràng, chuyên nghiệp**, phù hợp để làm tài liệu tham khảo cho các bạn sinh viên sau.

### 4. Lời cảm ơn chân thành

Em xin gửi lời cảm ơn chân thành đến:  
- **Giảng viên hướng dẫn** môn Lập trình mạng – Trường Đại học Công nghệ TP.HCM (HUTECH) – đã tận tình giảng dạy, định hướng đề tài và luôn hỗ trợ em trong suốt quá trình.  
- Các anh chị, bạn bè trong lớp đã cùng trao đổi, debug, động viên khi gặp khó khăn.  

Cảm ơn mọi người đã đồng hành cùng em trong hành trình này!

**Sinh viên thực hiện:** Nguyễn Trịnh Minh Huy  
**Khoa:** Công nghệ Thông tin – HUTECH  
**Ngày hoàn thành:** 23/12/2025  