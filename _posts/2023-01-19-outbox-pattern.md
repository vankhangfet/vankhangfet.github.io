---
layout: post
title: Outbox Pattern(phương thức thiết kế để lưu trạng thái và publish event đáng tin cậy)
tags: [Messaging]
---

# Outbox Pattern: Reliably Save State & Publish Events

# 1. What is outbox pattern: 
Đây là một mẫu thiết kế đảm bảo độ tin cậy khi bạn cần lưu trữ trạng thái vào trong database và publish message tới message broker. 
Pattern này giải quyết vấn đề gì? Bài toán đặt ra là khi bạn cần lưu trữ dữ liệu vào DB và sau đó push message vào message broker. Tuy nhiên database 
và message broker là 2 datasource khác nhau, như vậy để đảm bảo độ tin câỵ, chúng ta cần một distribution transaction để đảm bảo điều này. Outbox pattern sẽ giải quyết vấn đề này.
