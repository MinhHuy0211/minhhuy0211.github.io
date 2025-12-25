---
title: "Bài 1: Làm sao biết máy mình đang dùng IP gì trong Java?"
date: 2025-12-15
weight: 1
draft: false
tags: ["Java", "Network"]
summary: "Sử dụng class InetAddress để định danh máy tính."
---

Trong lập trình mạng, trước khi kết nối, ta phải biết "địa chỉ nhà" (IP) của mình và đối phương. Java cung cấp class `InetAddress` để làm việc này.

### Code lấy IP của máy (Localhost)
```java
import java.net.InetAddress;

public class MyIP {
    public static void main(String[] args) {
        try {
            InetAddress myIP = InetAddress.getLocalHost();
            System.out.println("Tên máy: " + myIP.getHostName());
            System.out.println("Địa chỉ IP: " + myIP.getHostAddress());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}