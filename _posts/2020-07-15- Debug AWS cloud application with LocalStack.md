---
layout: post
title: Debug AWS cloud application with LocalStack.
tags: [Cloud]
---

Phát triển ứng dụng trên Cloud sẽ đem lại rất nhiều lợi ích. Tuy nhiên trong quá trình phát triển việc Debug với Cloud sẽ tương đối khó khăn, vì các tài nguyên
đều nằm trên mạng Internet. Để giải quyết vấn đề về môi trường phát triển chúng ta có thể dùng LocalStack để debug, kiểm thử ứng dụng của chúng ta trước khi triển 
khai trên cloud. Vậy LocalStack là gì? Mời các bạn xem link sau:

LocalStack [https://github.com/localstack/localstack](https://github.com/localstack/localstack)

Chúng ta hãy thử sử dụng LocalStack qua ví dụ sau: Kịch bản là xây dựng một ứng dụng với SpringBoot, ứng dụng này sẽ lắng nghe message từ AWS SQS và cung cấp API cho phép người dùng gửi message tới AWS SQS. Trong ví dụ này mình có sử dụng source của github sau: 

 Spring AWS LocalStack [https://github.com/nylund/spring-aws-localstack](https://github.com/nylund/spring-aws-localstack)
 
 Các steps để thực hiện như sau:(Môi trường để thực hiện là Ubuntu 18.04 )
 
 1. Setup môi trường chạy LocalStack
 --> git clone https://github.com/localstack/localstack
     TMPDIR=/private$TMPDIR docker-compose up
 2. Build source code Spring Boot

 3. Create queue trên LocalStack 
 ~~~~
  aws --endpoint-url=http://localhost:4576 sqs create-queue --queue-name test_queue
 ~~~~
 4. Push message vào queue 
 ~~~~
 aws --endpoint-url=http://localhost:4576 sqs send-message --queue-url http://localstack:4576/000000000000/test_queue --message-body 'Test Message!'
 ~~~~
 5. Check debug log. 
 
 Chúng ta đã thấy debug log hiển thị message nhận được từ SQS. Ok vậy là có thể tin tưởng ứng dụng sẽ chạy trên AWS cloud rồi.
