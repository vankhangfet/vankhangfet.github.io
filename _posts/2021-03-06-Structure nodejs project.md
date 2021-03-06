---
layout: post
title:  Cấu trúc dự án cho Node Js
tags: [JS]
---

Thời gian gần đây mình có làm việc với Node JS, và có nhận thấy rằng với node js hay với javascript thì các project 
được tổ chức tương đối tự do. Nên post này mình có note lại một cấu trúc dự án theo cá nhân mình là tốt, để apply 
cho các dự án. Ngoài ra nó còn giúp cho bạn mở rộng ứng dụng dễ dàng. Chúng ta hãy xem cách tổ chức một dự án với Node js như sau: 

~~~~
src
│   app.js          # App entry point
└───api             # Express route controllers for all the endpoints of the app
└───config          # Environment variables and configuration related stuff
└───jobs            # Jobs definitions for agenda.js
└───loaders         # Split the startup process into modules
└───models          # Database models
└───services        # All the business logic is here
└───subscribers     # Event handlers for async task
└───types           # Type declaration files (d.ts) for Typescript
~~~~
Cấu trúc được chia thành các folder với những mục đích rõ ràng khác nhau. Cấu trúc trên cơ bản được triển khai theo mô các Layer sau

~~~~
    Controller 
        |
    Service Layer 
        |
    Data Access Layer
~~~~

Để giữ cho code trở lên dễ bảo trì, trong sáng chúng ta phải quan tâm đến những vấn đề sau:

1. Controller: 
   -> Chúng ta không thực hiện bussiness logic trong controller.
2. Service Layer
   -> Service Layer là nơi chúng ta triển khai bussiness do đó, Service Layer sẽ không gồm request/ response object. Service Layer cũng sẽ không chứa 
   các thành phần liên quan tới HTTP status, header. 
 
 Ngoài 2 điểm chinh trên, chúng ta nên kết hợp với những Pattern hay kỹ thuật sau :
  - Pub/Sub Layer 
  - Dependency Injection 
 
