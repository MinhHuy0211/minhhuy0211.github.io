---
title: "Bài 1: Làm sao biết máy mình đang dùng IP gì trong Java?"
date: 2025-12-15
weight: 1
draft: false
tags: ["Java", "Network", "InetAddress", "IP Address"]
summary: "Hướng dẫn chi tiết cách sử dụng class InetAddress để lấy địa chỉ IP của máy local, xử lý trường hợp nhiều card mạng và các lưu ý thực tế khi lập trình mạng."
thumbnail: "/sachhutech.jpg"  # Thêm nếu bạn có ảnh thumbnail
---

Trong lập trình mạng với Java, việc xác định địa chỉ IP của chính máy mình (localhost) là một trong những bước cơ bản nhất trước khi thiết lập kết nối socket, xây dựng server hay client. Java cung cấp class **`InetAddress`** trong package `java.net` để hỗ trợ việc này một cách đơn giản, mạnh mẽ và đáng tin cậy.

Bài viết này sẽ hướng dẫn bạn từ cách lấy IP cơ bản nhất đến xử lý các tình huống thực tế như máy có nhiều card mạng (Wi-Fi + Ethernet + VPN).

### 1. Giới thiệu về class `InetAddress`
`InetAddress` là lớp đại diện cho một địa chỉ IP (hỗ trợ cả IPv4 và IPv6). Đặc biệt:
- Không có constructor public → chỉ tạo được instance qua các phương thức static.
- Các phương thức chính thường dùng:
  - `InetAddress.getLocalHost()` → Lấy địa chỉ của máy hiện tại.
  - `InetAddress.getByName(String host)` → Lấy địa chỉ từ hostname hoặc IP string.
  - `InetAddress.getAllByName(String host)` → Lấy tất cả IP liên kết với một hostname.
  - `InetAddress.getLoopbackAddress()` → Trả về địa chỉ loopback (127.0.0.1 hoặc ::1).

### 2. Cách đơn giản nhất: Lấy IP và hostname của máy local
```java
import java.net.InetAddress;
import java.net.UnknownHostException;

public class MyLocalIP {
    public static void main(String[] args) {
        try {
            InetAddress localHost = InetAddress.getLocalHost();

            System.out.println("Hostname:             " + localHost.getHostName());
            System.out.println("Địa chỉ IP:           " + localHost.getHostAddress());
            System.out.println("Canonical Hostname:   " + localHost.getCanonicalHostName());

        } catch (UnknownHostException e) {
            System.err.println("Không thể xác định địa chỉ của máy local.");
            e.printStackTrace();
        }
    }
}