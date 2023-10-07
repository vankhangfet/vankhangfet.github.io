---
layout: post
title: Athena & Glue một service thú vị, nhưng cũng khá là khó hiểu?
tags: [Design]
---

Khi làm việc với Athena thì tôi thấy đây là một công cụ rất mạnh trong việc truy vấn dữ liệu, phân tích dữ liệu. 
Athena có thể truy vấn dữ liệu trên s3, dynamo db,etc. Hỗ trợ truy vấn phức tạp với SQL. Tuy nhiên mọi chuyện không hoàn toàn dễ dàng, 
và việc thiết kế với Athena làm tôi cảm thấy có chút khó hiểu? 

Vấn đề xảy ra khi tôi thực hiện truy vấn một bảng dữ liệu trong dynamo. Để thực hiện việc truy vấn này, các bạn sẽ cần triển khai theo infra như sau:
Refer: 

https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/access-query-and-join-amazon-dynamodb-tables-using-athena.html
![athena-lambda](https://docs.aws.amazon.com/images/prescriptive-guidance/latest/patterns/images/pattern-img/e6ff94af-d208-40c7-94e4-af257755a603/images/bc8e0132-b578-463b-bf55-3c39ce359c17.png "aws athena")

Kiến trúc này giúp bạn có thể thực hiện truy vấn SQL phức tạp như (join, group by,etc.) tới dynamo DB. Tuy nhiên có một vấn đề phát sinh tới schema đó là
để tạo ra schema của table thì Athena chỉ lấy mẫu một vài bản ghi trong DynamoDB để tạo ra schema. Do đó nếu như trong một table, các record có attribute khác nhau thì 
Athena sẽ có thể không thực hiện truy vấn tới attr này. 
Refer: 

https://github.com/awslabs/aws-athena-query-federation/issues/1346

https://stackoverflow.com/questions/74083235/new-dynamodb-attribute-cant-be-queried-from-athena

Sau khi dành thời gian tìm hiểu thì tôi được gợi ý cần phải tạo ra table trong Glue sau đó thực hiện query bằng Athena. Tuy nhiên tài liệu cũng khá đa dạng có 2 giải pháp 
được đưa ra. 

1. Dùng Glue Crawler để tạo ra table trong Database Catalog Glue.
2. Sẽ export data từ dynamo ra s3, sau đó sử dụng Athena query tới s3.

Sau khi rất nhiều try and fail tôi nhận thấy cần phải làm như sau: 

![athena-dynamo-s3](https://www.nordhero.com/posts/bi-pipeline/bi-pipeline-components.jpg "athena-dynamo-s3")




